<script>
  import InputText from 'primevue/inputtext';

  export default {
    name: 'FormUser',
    props: {
      user: {
        type: Object,
        default: () => ({}),
      }
    },
    data() {
      return {
        form: {
          name: '',
          phone: '',
          email: '',
          avatar: '',
        },
        selectedAvatar: null,
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
      async postContact() {
        console.log(this.form);
        await axios.post("http://localhost:8080/contacts", {
          contactName: this.form.name,
          contactEmail: this.form.email,
          contactPhone: this.form.phone,
          contactAvatar: this.selectedAvatar.code,}
        ).then(() => {
          alert("Contato adicionado com sucesso!")
          window.location.reload();
        }, (error) => {
          alert(error.response.data);
        });
      },
    },
  };

</script>

<template>
  <div class="form">
    <span id="boxes" class="p-input-icon-left">
      <i class="pi pi-user" />
      <InputText v-model="form.name" id="formInputs" type="text" placeholder="Nome" />
    </span>

    <span id="boxes" class="p-input-icon-left">
      <i class="pi pi-phone" />
      <InputText v-model="form.phone" id="formInputs" type="text" placeholder="Telefone" />
    </span>
    
    <span id="boxes" class="p-input-icon-left">
      <i class="pi pi-at" />
      <InputText v-model="form.email" id="formInputs" type="text" placeholder="E-mail" />
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

    <Button @click="postContact()" id="submit-button" label="Adicionar" icon="pi pi-check" class="p-button-warning p-button-raised p-button-rounded p-button-success"/>
  </div>
</template>

<style>
.form {
  display: flex;
  flex-direction: column;
  align-self: center;
  background-color: white;
  border-radius: 15px;
  margin-top: 70px;
  padding-block: 33px;
  padding-inline: 35px;
  box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2);
  border: 3px solid black;
}
#boxes {
  margin-block: 15px;
}
#formInputs {
  letter-spacing: 1px;
  height: 45px;
  width: 320px;
}
#submit-button {
  margin-top: 20px;
  letter-spacing: 1px;
  width: 70%;
  align-self: center;
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
