// @ts-nocheck
<script setup>

import {ref} from 'vue'

const showModal = ref(false)
const newNote = ref("")
const errorMessage = ref('');
const notes = ref([])
const date = new Date();
const options = { day: '2-digit', month: '2-digit', year: 'numeric' };
const malaysiaDateFormat = date.toLocaleDateString('en-GB', options).replace(/\//g, '/');
const close = () => {showModal.value = false}
function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 80%)";
}

// addNote function
const addNote = () => {
  if(newNote.value.length < 10) {
    return errorMessage.value = "Note needs to be at least 10 characters"
  }
  notes.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newNote.value,
    date: malaysiaDateFormat,
    backgroundColor: getRandomColor(), 
  })

  showModal.value = false
  newNote.value = ("")
  console.log(addNote)
}


</script>

<template>
  <main>
    <div id="modal1" v-if="showModal" tabindex="0" @keydown.esc="close" class="overlay">
      <div class="modal">
        <span class="errorMessage">{{ errorMessage }}</span>
        <textarea  
          v-model="newNote" @keydown.esc="close"
           @keydown.enter="addNote" 
           name="note" id="note" cols="30" rows="10"></textarea>
        <button @click="addNote">Add note</button>
        <button @click="showModal = false" @keydown.esc="close" class="close">
          Close
        </button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>MyNotes</h1>
        <button  @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes" :key="note.id" :style="{ backgroundColor: note.backgroundColor }" class="card">
          <p class="notes">{{ note.text }}</p>
          <p class="date">{{ note.date }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
  main {
    width: 100vw;
    height: 100vh;
    background-color: aliceblue;
  }

  .container {
    max-width: 1200px;
    padding: 10px;
    margin: 0 auto;
  }

  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  h1 {
    font-weight: bold;
    font-size: 75px;
    margin-bottom: 25px;
    color: black;
  }

  header button {
    width: 50px;
    height: 50px;
    border: none;
    background-color: black;
    color: white;
    padding: 10px;
    border-radius: 100%;
    cursor: pointer;
  }

  .card {
    width: 225px;
    height: 225px;
    background-color: orangered;
    border-radius: 15px;
    padding: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
    transition: all 0.3s ease-in-out;
    box-shadow: 0 10px 20px rgba(255, 95, 109, 0.2);
  }

  .card:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 30px rgba(255, 95, 109, 0.4);
}

  .date {
    text-align: right;
    font-size: 12.5px;
    font-weight: bold;
  }
  .cards-container {
    display: flex;
    flex-wrap: wrap;
  }

  .overlay {
    position: absolute;
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.77);
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .modal {
    max-width: 700px;
    background-color: white;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    padding: 30px;
    position: relative;
  }

  .modal button  {
    background-color: black;
    color: orange;
    border-radius: 10px;
    padding: 10px 30px;
    font-size: 20px;
    width: 100%;
    cursor: pointer;
    border: none;
    margin-top: 15px;

  }

  .modal .close {
    background-color: red;
    margin-top: 7px;
  }

  .errorMessage {
    color: red;
    margin-bottom: 5px;
  }
</style>>
