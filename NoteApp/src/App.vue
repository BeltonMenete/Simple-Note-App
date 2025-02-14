<script setup>
import { ref } from "vue";
console.clear();
const showModal = ref(false);
const newNote = ref("");
const notes = ref([]);

const getRandomLightColor = () => {
  const r = Math.floor(Math.random() * 156) + 100; // Ensures a light shade (100-255)
  const g = Math.floor(Math.random() * 156) + 100;
  const b = Math.floor(Math.random() * 156) + 100;
  return `#${r.toString(16).padStart(2, "0")}${g.toString(16).padStart(2, "0")}${b.toString(16).padStart(2, "0")}`;
};
const addNote = () => {
  notes.value.push({
    id: Math.floor(Math.random() * 1000000000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: getRandomLightColor(),
  });
  showModal.value = false;
  newNote.value = "";
};
</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model="newNote" name="note" id="note" rows="10"></textarea>
        <button @click="addNote()">Add note</button>
        <button class="close" @click="showModal = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes" class="card" :style="{ backgroundColor: note.backgroundColor }" :key="note.id">
          <p class="main-text">{{ note.text.toString() }}</p>
          <p class="date">
            {{ note.date.toLocaleDateString("en-us") }}
          </p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Sansita&display=swap");
* {
  font-family: "Sansita", serif;
}
.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: #000000c4;
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: absolute;
  display: flex;
  flex-direction: column;
}
.modal button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: #15ff00;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 7px;
}
.modal .close {
  background-color: #ff0000e8;
}
.modal .close:hover {
  background-color: #ff0000a6;
}
.modal button:hover {
  background-color: #36d443bb;
}
main {
  height: 100vh;
  width: 100vw;
}

.container {
  max-width: 1000px;
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
  margin-bottom: 25px;
  font-size: 75px;
}

header button {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: #151414;
  border-radius: 100%;
  color: white;
  font-size: 20px;
  font-family: "Courier New", Courier, monospace;
}
button:hover {
  background-color: #151414d2;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
}

.card {
  width: 225px;
  height: 225px;
  background-color: #edb62c;
  border-radius: 20px;
  padding: 10px;
  padding-left: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
  font-family: "Sansita", serif;
  font-weight: lighter;
  font-style: normal;
  word-wrap: break-word;
}

.date {
  font-size: 12px;
  font-weight: bold;
}
</style>
