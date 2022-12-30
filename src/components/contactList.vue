<template>
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
</template>

<script>
    export default {
        
    }
</script>

<style>

</style>