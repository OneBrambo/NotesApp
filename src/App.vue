<script setup lang="ts">

import {ref} from "vue";

const showModal = ref(false);
const newNote = ref("");
const notes : any = ref([]);
function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}
const addNote = () => {
  notes.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newNote.value,
    date: new Date(),
    bgColor: getRandomColor(),
  })
  showModal.value = false;
  newNote.value = "";
}
</script>

<template>
  <main>

    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model="newNote" name="note" id="note" cols="30" rows="10" placeholder="Inserisci qui la tua nota"></textarea>
        <button @click="addNote">Add Note</button>
        <button class="close" @click="showModal = false">Close</button>

      </div>
    </div>

    <div class="container">
      <header>
        <h1>Note</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes"  class="card" :style="{backgroundColor: note.bgColor}">
          <p class="main-text">{{note.text}}</p>
          <p class="date">{{note.date.toLocaleDateString()}}</p>
        </div>

      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100vh;
  width: 100vw
}

.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
}

header button {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(21,20,20);
  border-radius: 100%;
  color: white;
  font-size: 20px;
}

.card {
  width: 225px;
  height: 225px;
  background-color: blue;
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}

.date {
  font-size: 12.5px;
  font-weight: bold;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;

}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.50);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  width: 750px;
  background-color: darkslategray;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}
textarea{
  background-color: white;
  color: black;
  border-radius: 10px;
}
.modal button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: darkgreen;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px
}

.modal .close {
  background-color: darkred;
  margin-top: 7px;
}
</style>