<template>
  <div id="app">
    <form @submit.prevent>
      <div class="title">
        <i class='bx bxs-contact'></i>
        <h1>Список Контактов</h1>
      </div>
      <input v-model="name"  type="text" placeholder="Имя">
      <input v-model="num" type="number" placeholder="Номер телефона">
      <input v-model="email" type="email" placeholder="Email адрес">
      <button @click="addContact">Создать</button>
    </form>
    <div class="contact__list">
      <div class="contact" v-for="(contact, index) in contacts" v-bind:key="index">
        <i class='bx bxs-contact'></i>
        <div class="contact__info">
          <h4>Имя контакта</h4>
          <input type="text" v-model="contact.name">
          <h4>Номер контакта</h4>
          <input type="text" v-model="contact.num">
          <h4>Email адрес контакта</h4>
          <input type="text" v-model="contact.email">
        </div>
        <div class="btn">
          <button class="btn__edit" @click="editContact()">Изменить</button>
          <button class="btn__delete" @click="removeContact(index)">Удалить</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      editButton: true,
      contacts: [
        { id: 1, name: 'John', num: +998912831617, email: 'jonnn@gmail.com' },
        { id: 2, name: 'Mice', num: +998912831617, email: 'test@gmail.com' },
        { id: 3, name: 'Niko', num: +998912831617, email: 'nikkkk@gmail.com' },
        { id: 4, name: 'Said', num: +998912831617, email: 'saidd@gmail.com' },
        { id: 5, name: 'Kerry', num: +998912831617, email: 'kerry@gmail.com' },
        { id: 6, name: 'Bill', num: +998912831617, email: 'bill123@gmail.com' },
      ],
      name: '',
      num: '',
      email: ''
    }
  },

  created() {
    const contactsData = localStorage.getItem('contact-list')

    if (contactsData) {
      this.contacts = JSON.parse(contactsData)
    }
  },




  mounted() {
    if (localStorage.getItem('contact-list')) {
      try {
        this.contacts = JSON.parse(localStorage.getItem('contact-list'));
      } catch (e) {
        localStorage.removeItem('contact-list');
      }
    }
  },




  methods: {
    addContact() {
      const newContact = {
        id: Date.now(),
        name: this.name,
        num: this.num,
        email: this.email
      } 
      if (this.name.length && this.num.length && this.email.length) {
        this.contacts.push(newContact)

        localStorage.setItem('contact-list', JSON.stringify(this.contacts))

      }
      this.num = ''
      this.name = ''
      this.email = ''
      this.saveContacts()
    }, 

    removeContact(index) {
      this.contacts.splice(index, 1)
      this.saveContacts()
    },

    editContact() {
      this.saveContacts()
      alert('Данные успешно изменены и сохранены')
    },

    saveContacts() {
      const parsed = JSON.stringify(this.contacts);
      localStorage.setItem('contact-list', parsed);
    }
  }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  i {
    font-size: 40px;
  }

  
  form {
    margin: auto;
    width: 50%;
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  input {
    width: 100%;
    margin-bottom: 10px;
    padding: 10px 15px; 
  }

  button {
    width: 100%;
    padding: 10px 15px;
    color: white;
    background: #000;
    cursor: pointer;
  }

  .title {
    display: flex;
    align-items: center;
    gap: 20px;
    margin-bottom: 20px;
  }

  .contact__list  {
    padding: 50px;
    display: grid;
    grid-gap: 10px;
    grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  }

  .contact {
    display: flex;
    align-items: center;
    justify-content: space-around;
    border: 1px solid teal;
    gap: 5px;
    padding: 20px;
  }

  .contact i {
    font-size: 4rem;
  }
  
  .contact__info h4 {
    font-size: 1rem;
  }

  .contact__info h4 input {
    border: none;
    padding: 0;
    margin: 5px;
  }

  .btn {
    display: flex ;
    flex-direction: column;
    gap: 5px;
  }

  .btn__edit{
    background-color: teal;
  }
  
  .btn__delete {
    background-color:rgb(241, 66, 66);
  }
</style>  
