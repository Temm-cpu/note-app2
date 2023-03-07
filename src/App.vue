<template>
  <div class="totalty">
    <header>
      <div class="heading">
        <h1>TAKE A NOTE 🖊</h1>
        <button class="add" @click="isvisibleon">
          📕
        </button>
      </div>
    </header>

    <main class="createcontiner">
      <div class="create" v-if="isvisible">
        <input
          class="title"
          type="text"
          placeholder="TITLE"
          v-model="pagetitle"
        />
        <textarea
          v-model="note"
          class="text-area"
          name="note"
          id="note"
          cols="30"
          rows="10"
        ></textarea>
        <button class="add-note" @click="addnote">ADD NOTE</button>
        <button class="cancel" @click="cancelall">CANCEL</button>
      </div>
    </main>
    <div class="flex">
      <div class="content-container" v-for="note in noteTaken">
        <h2>{{ note.title }}</h2>
        <p class="content" v-if="textvisible">
          {{ note.text }}
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
let isvisible = ref(false);
let textvisible = ref(false);
const note = ref("");
const noteTaken = ref([]);
const pagetitle = ref("");
function isvisibleon() {
  isvisible.value = true;
}
function cancelall() {
  isvisible.value = false;
}
function addnote() {
  const newnote = {
    text: note.value,
    title: pagetitle.value,
    id: Math.random * 1000000000,
  };

  noteTaken.value.push(newnote);
  note.value = "";
  pagetitle.value = "";
  console.log(note.value);
  console.log(pagetitle.value);
  textvisible.value = true;
  isvisible.value = false;
}
</script>
<style scoped>
.totalty {
  background: url(./image/home.webp);
  height: 100vh;
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}
.title,
.title::placeholder {
  text-align: center;
  color: snow;
  background-color: brown;
}

.heading {
  display: flex;
  justify-content: space-between;
  background: 2px solid black;
}

.add {
  background-color: burlywood;
  margin: 2rem;
  border: 2px dotted brown;
  border-radius: 10px;
  padding: 10px;
  font-size: 3rem;
}
.add:hover {
  box-shadow: 0 0 5px 10px rgba(133, 124, 124, 0.575);
}
h1 {
  margin: 2rem;
  border: 2px solid brown;
  background-color: burlywood;
  padding: 10px;
}

main {
  display: flex;
}
.content-container {
  border: 2px solid black;
  background-color: black;
  color: white;
  /* width: 20%; */
  border-radius: 10px;
  margin: 5px;
  height: 10rem;
  padding: 1rem;
  /* overflow: scroll; */
  display: grid;
  align-items: center;
}
.createcontainer {
  display: relative;
  align-items: center;
}
.text-area {
  background-color: aqua;
  border-radius: 5px;
}
.create {
  align-items: center;
  display: grid;
  /* border: 2px solid brown; */
  width: 90%;
  text-align: center;
  gap: 5px;
  z-index: 2;
  margin-left: auto;
  margin-right: auto;
  margin-top: 2rem;
}
.add-note {
  background-color: aqua;
  border-radius: 5px;
}
.cancel {
  background-color: red;
  border-radius: 5px;
}
.flex {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  /* margin: auto auto; */
}
</style>
