<script setup>
import { ref } from 'vue';
const showModal = ref(false);
const newNote = ref("");
const errormessage = ref("");
const notes = ref([]);
function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
 
}
const addNote = () => {
  if(newNote.value.length <= 9){
    return errormessage.value = "Note need to min 10 character Long"
  }
  notes.value.push ({
    id:Math.floor(Math.random()*100000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: getRandomColor()
  })
  showModal.value = false;
  newNote.value=""
  errormessage.value = ""
}

</script>
<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <h5 @click="showModal = false">x</h5>
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <p v-if="errormessage" style="color: red;">{{ errormessage }}</p>
        <button @click="addNote">Add Note</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes" class="card"  :key="note.id"  :style="{backgroundColor: note.backgroundColor}">
          <p class="main-text">{{ note.text }}</p>
          <p class="date" style="font-weight: bold;">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
  .container {
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto
  }

  h1 {
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }

  .card {
    width: 225px;
    height: 225px;
    background-color: rgb(237, 182, 44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
  }

  .main-text {
    line-height: 1.25;
    font-size: 17.5px;
    font-weight: bold;
  }

  .date {
    font-size: 12.5px;
    margin-top: auto;
  }

  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  header button {
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: rgb(21, 20, 20);
    border-radius: 1000px;
    color: white;
    font-size: 30px;
    text-align: center;
  }
  .cards-container {
    display: flex;
    flex-wrap: wrap;
  }

  .overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.77);
    transform: translate(-50%, -50%);
    top: 50%;
    left: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 10;
  }

  main {
    height: 100vh;
     background: url("https://www.maketecheasier.com/assets/uploads/2021/03/change-note-background-ios-featured.jpg");
     background-repeat: no-repeat;
  background-size: cover;
   background-position: center;
   overflow: hidden;
   overflow-y: scroll;
  }

  .modal {
    width: 750px;
    background-color: white;
    border-radius: 10px;  
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }

  .modal button {
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;

  }

  .modal h5 {
    margin-left: auto;
    font-size: 20px;
    z-index: 100000;
    cursor: pointer;
  }

  textarea {
    width: 100%;
    height: 200px;
    padding: 5px;
    font-size: 20px;
  }
</style>