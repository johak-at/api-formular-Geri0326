<script setup>

import { onMounted, ref } from 'vue';
import PocketBase from 'pocketbase';

const pb = new PocketBase("https://pb.seiwald.club");
const studentList = ref([]);
const newVorname = ref("");
const newNachname = ref("");
const newOrt = ref("");
const newGeburtsDatum = ref(null);

onMounted(async () => {

    getStudents();

})

async function getStudents()
{

const data = await pb.collection("4bhk").getFullList();
studentList.value = data;

}

async function createStudent()
{
    const newStudent = {
            vorname: newVorname.value,
            nachname: newNachname.value,
            wohnort: newOrt.value,
            geburtstag: newGeburtsDatum.value
    }
    await pb.collection('4bhk').create(newStudent);
    vorname.value = "";
    nachname.value = "";
    wohnort.value = "";
    geburtsdatum.value = "";
    getStudents();
}

async function deleteStudent(id)
{
    await pb.collection("4bhk").delete(id);
    getStudents();
}


</script>



<template>

    <h1>Our Students</h1>
    

    <ul>

        <li v-for="student in studentList" :key="student.id">

            {{ student.vorname }} {{ student.nachname }}
            wohnt in {{ student.wohnort }} und ist am {{ student.geburtstag.substring(0,10) }} geboren.
            <button @click="deleteStudent(student.id)">X</button>

        </li>

    </ul>
    <form action="">
    <div>
    <label for="vorname"></label>
    <input v-model="newVorname"  type="text" placeholder="vorname eingeben">&nbsp;
    </div>
    <div>
    <label for="nachname"></label>
    <input v-model="newNachname"  type="text" placeholder="nachname eingeben">&nbsp;
    </div>
    <div>
    <label for="wohnort"></label>
    <input v-model="newOrt"  type="text" placeholder="Wohnort eingeben">&nbsp;
    </div>
    <div>
    <label for="geburtsdatum"></label>
    <input v-model="newGeburtsDatum"  type="date" placeholder="nachname eingeben">&nbsp;
    </div>
    <button @click.prevent="createStudent">Add Student</button>
    </form>



</template>