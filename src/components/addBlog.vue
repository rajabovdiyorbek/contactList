<template>
    <form @submit.prevent>
        <div class="title">
            <i class='bx bxs-contact'></i>
            <h1>Список Контактов</h1>
        </div>
            <input v-model="name" type="text" placeholder="Имя">
            <input v-model="num" type="number" placeholder="Номер телефона">
            <input v-model="email" type="email" placeholder="Email адрес">
            <button @click="addContact">Создать</button>
    </form>
</template>

<script>
    export default {
        
    }
</script>

<style>

</style>