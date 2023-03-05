<script setup>
import { ref } from 'vue';
let showModule = ref(false);
const newNote = ref('');
const notes = ref([]);

function randomColor() {
  var rc = (~~(Math.random() * 0xFFFFFF)).toString(16);
  return '#' + new Array(7 - rc.length).join('0') + rc;
}


function addNewNote() {

  //Close the popup
  showModule.value = false;

  //get the inpuut value
  const noteValue = {
    id:Math.floor(Math.random() * 1000000),
    txt: newNote.value,
    date: new Date,
    backgroundColor:randomColor()
  };

  //push it in notes
  notes.value.push(noteValue);

  // 
  newNote.value = ''
}


</script>


<template>
  <div class="overlay" v-show="showModule">
    <div class="module">
      <textarea name="note" id="note" cols="30" rows="10" v-model="newNote"></textarea>
      <button class="add" @click='addNewNote()'>Add Note</button>
      <button class="close " @click='showModule = false'>Close</button>
    </div>
  </div>
  <div class="main">
    <div class="container">

      <header>
        <h1>Notes</h1>
        <button @click='showModule = true'>+</button>
      </header>

      <div class="cards-container">
        <div class="card" v-for="note in notes">
          <p class="main-text"> {{note.txt}}</p>
          <p class="date">{{note.date.toLocaleDateString()}}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.main {
  height: 100vh;
  width: 100vw;
  background-image: url('./note.jpg');
  background-size: cover;

}
.container{
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;


}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
h1{
  font-size: 50px;
  font-weight: 900;
  color: rgb(246, 246, 173);
}
header button{
  border: none;
  width: 50px;
  height: 50px;
  border-radius: 100%;
  font-size: 20px;
  background-color: black;
  color: white;
  font-weight: bold;
  cursor: pointer;
}
.card {
  padding: 10px;
  display: flex;
  flex-direction: column;
  margin-right: 10px;
  margin-bottom: 10px;
  border-radius: 15px;
  width: 250px;
  height: 250px;
  background-color: black;
  color: white;
  justify-content: space-between;

}
.main-text{
  color: rgb(166, 169, 172);

}
.date{
  font-weight: bold;
}
.cards-container{
  display: flex;
  flex-wrap: wrap;
}
.overlay{
  width: 100%;
  height: 100%;
  position: absolute;
  background-color: rgba(0, 0, 0, 0.77);
  z-index: 10;
  display: flex;
  justify-content: center;
  align-items: center;

}
.module{
  width: 750px;
  position: relative;
  background-color: white;
  display: flex;
  padding: 30px;
  flex-direction: column;

}
.module .add{
  cursor: pointer;
  color: white;
  background-color: rgb(16, 16, 35);
  margin-top: 7px;
  font-weight: bold;
  width: 100%;
  padding: 10px 20px;
  border: none;
  font-size: 20px;

}
.module .close{
  cursor: pointer;
  color: white;
  background-color: rgba(234, 211, 8, 0.645);
  margin-top: 7px;
  font-weight: bold;
  width: 100%;
  padding: 10px 20px;
  border: none;
  font-size: 20px;
}

</style>