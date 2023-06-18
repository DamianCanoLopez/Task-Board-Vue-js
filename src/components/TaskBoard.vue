<script setup>
import { reactive, onMounted, watch } from "vue";
import InputNew from "./InputNew.vue";

// const count = ref(0);
const boards = reactive([]);

function startDrag(evt, boardId, itemId) {
  console.log(boardId, itemId);
  evt.dataTransfer.dropEffect = "move";
  evt.dataTransfer.effectAllowed = "move";
  evt.dataTransfer.setData("item", JSON.stringify({ boardId, itemId }));
}
function onDrop(evt, dest) {
  const { boardId, itemId } = JSON.parse(evt.dataTransfer.getData("item"));
  console.log({ boardId, itemId });
  const board = boards.find((board) => board.id === boardId);
  const itemIndex = board.items.findIndex((item) => item.id === itemId);

  if (itemIndex > -1) {
    const [item] = board.items.splice(itemIndex, 1);
    dest.items.push({ ...item });
  }
}

function handleNewItem(text, board) {
  console.log(text.value);
  board.items.push({ id: crypto.randomUUID(), title: text.value });
}

function createNewBoard() {
  const name = prompt("Name of board");
  if (name) {
    const board = {
      id: crypto.randomUUID(),
      name: name,
      items: [],
    };

    boards.push(board);
  }
}

function deleteBoard(board) {
    const boardIndex = boards.indexOf(board);

    if(boardIndex > -1){
        boards.splice(boardIndex, 1);
    }
}

function deleteItem(board, item) {
    const itemIndex = board.items.indexOf(item);

    if(itemIndex > -1){
        board.items.splice(itemIndex, 1);
    }
}

watch(boards, (newVal) => {
  localStorage.setItem('boards', JSON.stringify(newVal));
}, { deep: true });

onMounted(() => {
  const storedBoards = JSON.parse(localStorage.getItem('boards'));
  if (storedBoards) {
    boards.push(...storedBoards);
  }
});
</script>

<template>
  <div class="container">
    <nav>
      <span class="create-boards-btn">
        <button id="create-btn" @click="createNewBoard">Create list</button>
      </span>
    </nav>

    <div class="boards-container">
      <div class="boards">
        <div
          class="board"
          @drop="onDrop($event, board)"
          @dragover.prevent
          @dragenter.prevent
          v-for="board in boards"
          :key="board.id"
        >
          <h3>{{ board.name }}</h3>
          <button @click="deleteBoard(board)">Delete Board</button>
          <div class="input">
            <InputNew @on-new-item="(text) => handleNewItem(text, board)" />
          </div>
          <div
            class="item drag-el"
            draggable="true"
            @dragstart="startDrag($event, board.id, item.id)"
            v-for="item in board.items"
            :key="item.id"
          >
            {{ item.title }}
            <button @click="deleteItem(board, item)">Delete Item</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

.container {
  background-color: #f5f5f5;
  padding: 20px;
  margin: 0 auto;
  max-width: 1200px;
  border-radius: 1%;
}

.board {
    display: flex;
    flex-direction: column;
    background: #ffffff;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.299);
    margin: 3%;
    color:#000;
}

.board:hover{
    box-shadow: 3px 7px 10px -2px rgb(149, 50, 211);
}

.item {
  background-color: #ffffff;
  padding: 5%;
  margin-top: 3%;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.299);
}

.item:hover{
    background-color: #0000005f;
    color: #ffffff;
}

button {
    background-color: rgba(22, 18, 18, 0.811);
    color: #ffffff;
    border: none;
    padding: 5px 10px;
    border-radius: 5px;
    cursor: pointer;
    margin-bottom: 3%;
}

button:hover{
    background-color: rgb(255, 2, 2);
    color: #000;
}

nav{
    display: flex;
    justify-content: center;
    padding: 1%;
    margin: 1%;
}

nav:hover{
    background-color: #1b161679;
}

h3{
    text-align: center;
}


#create-btn{
    margin: 2%;
    background-color: rgba(22, 18, 18, 0.811);
}

#create-btn:hover{
    box-shadow: 3px 7px 10px -2px rgb(224, 69, 18);
    color: #f6f6f6;
}

.drop-zone {
  background-color: #eee;
  margin-bottom: 10px;
  padding: 10px;
}
.drag-el {
  background-color: #fff;
  margin-bottom: 10px;
  padding: 5px;
}

.boards {
    display: flex;
  flex-wrap: wrap;
}


@media screen and (max-width: 768px) {
  .boards {
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
}
</style>