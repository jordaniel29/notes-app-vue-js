<script>
import CardNote from "../components/CardNote.vue";

export default {
  name: "ListNode",
  components: { CardNote },
  methods: {
    closeList() {
      this.$emit("close");
    },
    addNote() {
      this.$emit("add");
    },
    changeSelectedNote(id) {
      this.$emit("changeSelected", id);
    },
    search() {
      var search = document.getElementsByClassName("search-box")[0].value;
      this.$emit("search", search);
    },
  },
  props: ["list", "noteSelected"],
};
</script>

<template>
  <div class="backdrop" @click.self="closeList()">
    <div class="container">
      <div class="head">
        <div class="head-title">Notes</div>
        <div class="head-add" @click="addNote">+</div>
      </div>
      <input type="text" class="search-box" @input="search" />
      <div class="list" v-for="note in list.slice().reverse()" :key="note.id">
        <CardNote
          :title="note.title"
          :body="note.body"
          :date="note.date"
          :selected="note.id == noteSelected"
          :first="note.id == 0"
          :last="note.id == list.length - 1"
          @click="changeSelectedNote(note.id)"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
.backdrop {
  background-color: rgba(0, 0, 0, 0.7);
  position: fixed;
  top: 0;
  width: 100%;
  max-width: 1024px;
  height: 100%;
}
.container {
  background-color: #141414;
  width: 400px;
  height: 100vh;
  padding: 15px;
  font-size: 16px;
  color: #fff;
  overflow-y: scroll;
}
.head {
  display: flex;
  justify-content: space-between;
  font-weight: 700;
  font-size: 25px;
}
.head-title {
  color: #fff;
}
.head-add {
  color: #ffd52e;
  cursor: pointer;
}
.search-box {
  margin-top: 10px;
  margin-bottom: 8px;
  background-color: #ffffff14;
  border: none;
  border-radius: 3px;
  padding: 8px;
  width: 100%;
  box-sizing: border-box;
  color: white;
}
.search-box:focus {
  outline-color: #ffd52e;
}
.list {
  border-radius: 3px;
  background-color: #ffffff14;
}

@media only screen and (max-width: 768px) {
  .container {
    width: 100vw;
    box-sizing: border-box;
  }
}
</style>
