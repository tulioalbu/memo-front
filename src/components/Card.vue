<script>
  import UpdateUser from "./UpdateUser.vue";

  export default {
    name: "Card",
    data() {
      return {
        showForm: false,
        cardUser: {
          name: this.cardName,
          phone: this.cardPhone,
          email: this.cardEmail,
          avatar: this.cardAvatar,
          id: this.cardId,
        },
      }
    },
    props: {
      cardName: String,
      cardPhone: String,
      cardEmail: String,
      cardAvatar: String,
      cardId: String,
    },
    components: {
      UpdateUser,
    },
    methods: {

      async deleteContact(id) {
        let w = window.confirm("Você realmente deseja deletar este contato?");
        if (w) {
          await axios.delete(`http://localhost:8080/contacts/${id}`)
          alert("Contato deletado com sucesso!")
          window.location.reload();
        }
      },
    },
  }
  
</script>

<template>

  <div id="card" :style="showForm === true ? 'filter: brightness(60%);' : '' " >
    <div class="infos">
      <img class="img" :src="`./src/assets/${cardAvatar}.png`" alt="">
  
      <div class="info">
        <span>{{cardName}}</span>
        <span>{{cardPhone}}</span>
        <span>{{cardEmail}}</span>
      </div>
    </div>

    <div class="buttons">
      <i @click="showForm = true" id="button" style="font-size: 2.3rem" class="pi pi-user-edit" />
      <i @click="deleteContact(cardId)" id="button" style="font-size: 2.3rem" class="pi pi-times-circle" />
    </div>
  </div>

  <UpdateUser class="update" v-if="showForm" :userId="cardId" :userName="cardName" :userPhone="cardPhone" :userEmail="cardEmail" :userAvatar="cardAvatar" />

</template>

<style>
  #card {
    display: flex;
    background-color: white;
    height: 110px;
    width: 490px;
    border-radius: 10px;
    margin-inline: 95px;
    padding-inline: 8px;
    justify-content: space-between;
    margin-bottom: 27px;
    box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2);
    border: 3px solid black;
  }
  .img {
    display: flex;
    width: 20%;
    align-self: center;
  }
  .infos {
    display: flex;
    flex-direction: row;
    align-self: center;

  }
  .info {
    display: flex;
    flex-direction: column;
    align-self: center;
    letter-spacing: 2px;
    margin-left: 10px;
  }
  .buttons {
    display: flex;  
    align-items: center;
  }
  #button {
    display: flex;
    align-items: center;
    margin-inline: 5px;
    cursor: pointer;
  }
  .update {
    position: absolute;
    top: 5%;
    right: 9%;
  }

</style>