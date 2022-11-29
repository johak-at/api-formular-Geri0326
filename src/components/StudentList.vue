<script setup>
import {ref} from "vue";
const studentList = ref();
onMounterd(async () => {
  const response = await fetch("https://pb.seiwald.club/api/collections/4bhk/records")
    const data = await response.json();
    studentList.value = data.records;
}

);
</script>

<template>
    <h1>Our Students</h1>
    
    <ul>
        <li v-for="student in studentList" >
            {{ student.name }}
        </li>
    </ul>
</template>