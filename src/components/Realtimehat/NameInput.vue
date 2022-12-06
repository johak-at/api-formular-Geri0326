<script setup>
import { ref} from "vue";
const emits = defineEmits(["setUserName"]);
const userName = ref("");

</script>

<template>
    <h2>Hello Friend! What's your name?</h2>
    <input v-model="userName" type="text" placeholder="Enter Username" @keyup.enter="emits('setUserName', userName)"> &nbsp;
    <button @click="emits('setUserName', userName)">Set Username</button>
</template>