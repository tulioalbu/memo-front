<script>
  import axios from "axios";

  export default {
  name: "App",
    data() {
      return {
        contacts: [],
        userContact: {},
      };
    },
    methods: {
      async getContacts() {
        await axios.get("http://localhost:8080/contacts").then((response) => {
          console.log(response.data)
          this.contacts = response.data;
        });
      },
      async getContact(id) {
        await axios.get(`http://localhost:8080/contacts/${id}`).then((response) => {
          console.log(response.data)
          this.userContact = response.data;
        });
      },
    },
    mounted() {
      this.getContacts();
    },
  };

</script>

<template>
  <div id="cols">
    <div class="col-a">
      <Header/>
      <FormUser class="formPosition"/>
    </div>

  <div class="col-b">
    <div v-for="contact in contacts.reverse()" v-bind:key="contact.contactId" >
      <Card 
        :cardName="`${contact.contactName}`" 
        :cardPhone="`${contact.contactPhone}`" 
        :cardEmail="`${contact.contactEmail}`"
        :cardAvatar="`${contact.contactAvatar}`"
        :cardId="`${contact.contactId}`"
      />
    </div>
  </div>

  </div>


</template>

<style>
  #cols {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin-block: 50px;
    margin-inline: 80px;
  }
  .col-a {
    display: flex;
    flex-direction: column;
  }
  .col-b {
    display: flex;
    flex-direction: column;
    box-sizing: border-box;
    max-height: 840px;
    overflow-y: auto;
  } 
</style>
