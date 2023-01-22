<script> 
  import InputText from 'primevue/inputtext';

  export default {
    name: 'UpdateUser',
    props: {
      userId: String,
      userName: String,
      userPhone: String,
      userEmail: String,
      userAvatar: String,
    },
    data() {
      return {
        form: {
          name: this.userName,
          phone: this.userPhone,
          email: this.userEmail,
          avatar: this.userAvatar,
        },
        selectedAvatar: {name: "Avatar " + this.userAvatar, code: this.userAvatar},
        avatars: [
          {name: 'Avatar 1', code: '1'},
          {name: 'Avatar 2', code: '2'},
          {name: 'Avatar 3', code: '3'},
          {name: 'Avatar 4', code: '4'},
          {name: 'Avatar 5', code: '5'},
          {name: 'Avatar 6', code: '6'},
          {name: 'Avatar 7', code: '7'},
          {name: 'Avatar 8', code: '8'},
          {name: 'Avatar 9', code: '9'},
          {name: 'Avatar 10', code: '10'},
          {name: 'Avatar 11', code: '11'},
          {name: 'Avatar 12', code: '12'},
          {name: 'Avatar 13', code: '13'},
          {name: 'Avatar 14', code: '14'},
        ]
      };
    },
    methods: {
      async updateContact(id) {
        console.log(this.form);
        await axios.put(`http://localhost:8080/contacts/${id}`, {
          contactName: this.form.name,
          contactEmail: this.form.email,
          contactPhone: this.form.phone,
          contactAvatar: this.selectedAvatar.code,}
        ).then(() => {
          alert("Contato modificado com sucesso!")
          window.location.reload();
        }, (error) => {
          alert(error.response.data);
        });
      },
      closeWindow() {
        window.location.reload();
      }
    },
  };

</script>

<template>
  <div class="updateform">
    
    <i @click="closeWindow()" id="closeWindow" class="pi pi-times" />

    <span id="boxes" class="p-input-icon-left">
      <i class="pi pi-user" />
      <InputText v-model="form.name" id="updateInputs" type="text" :placeholder="userName" />
    </span>

    <span id="boxes" class="p-input-icon-left">
      <i class="pi pi-phone" />
      <InputText v-model="form.phone" id="updateInputs" type="text" :placeholder="userPhone" />
    </span>
    
    <span id="boxes" class="p-input-icon-left">
      <i class="pi pi-at" />
      <InputText v-model="form.email" id="updateInputs" type="text" :placeholder="userEmail" />
    </span>

    <Dropdown id="boxes" v-model="selectedAvatar" :options="avatars" optionLabel="name" placeholder="Escolha o avatar" :showClear="true">
      <template #value="avatars">
        <div id="select" v-if="avatars.value">
            <img class="avatarImg" :src="`./src/assets/${avatars.value.code}.png`" alt="" />
            <span>{{avatars.value.name}}</span>
        </div>
        <span v-else>
            {{avatars.placeholder}}
        </span>
      </template>
    </Dropdown>
    <Button @click="updateContact(userId)" id="update-button" label="Modificar" icon="pi pi-check" class="p-button-warning p-button-raised p-button-rounded p-button-success"/>
  </div>
</template>

<style>
.updateform {
  display: flex;
  flex-direction: column;
  align-self: center;
  border-radius: 15px;
  margin-top: 70px;
  padding-block: 33px;
  padding-inline: 35px;
  box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2);
  border: 3px solid black;
  background-color: #a2a2a2;
  background-size: cover;
}
.bg {
background-repeat: cover;
z-index: 1;
}
#updateInputs {
  letter-spacing: 1px;
  height: 45px;
  width: 320px;
}
#update-button {
  margin-top: 20px;
  letter-spacing: 1px;
  width: 70%;
  align-self: center;
  background-color: white;
}
#closeWindow {
  position: absolute;
  transform: scale(1.5);
  right: 0;
  top: 0;
  margin: 20px;
  cursor: pointer;
}
.avatarImg {
  display: flex;
  margin-right: 10px;
  width: 15%;
  align-self: center;
}
#select {
  display: flex;
  align-items: center;
}
.p-dropdown.p-dropdown-clearable .p-dropdown-label {
  letter-spacing: 1px;
  max-width: 280px;
  height: 55px;
}
</style>
