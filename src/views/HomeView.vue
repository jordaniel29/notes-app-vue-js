<script>
import ListNotesVue from "../components/ListNotes.vue";
import DetailNote from "../components/DetailNote.vue";
import ListVue from "../models/List.vue";

export default {
  name: "HomeView",
  components: { ListNotesVue, DetailNote },
  data() {
    return {
      showList: true,
      notesList: ListVue.notesList,
      noteSelected: ListVue.notesList.length - 1,
    };
  },
  methods: {
    toggleList() {
      this.showList = !this.showList;
    },
    addNote() {
      this.noteSelected = this.notesList.length;
      const date = new Date();
      const options = { day: "numeric", month: "long", year: "numeric" };
      const fDate = date.toLocaleDateString("en-US", options);
      this.notesList.push({
        id: this.noteSelected,
        title: "",
        body: "",
        date: fDate,
      });
      this.showList = !this.showList;
    },
    changeSelected(value) {
      this.noteSelected = value;
      this.showList = !this.showList;
    },
    changeTitle(title) {
      this.notesList[this.noteSelected].title = title;
    },
    changeBody(body) {
      this.notesList[this.noteSelected].body = body;
    },
    search(value) {
      let filter = value.toUpperCase();
      let list = document.getElementsByClassName("card-note");

      for (let i = 0; i < list.length; i++) {
        // Search by Title
        let a = list[i].getElementsByClassName("note-title")[0];
        let txtValue = a.textContent || a.innerText;
        if (txtValue.toUpperCase().indexOf(filter) > -1) {
          list[i].style.display = "";
        } else {
          list[i].style.display = "none";
        }

        // Search by Content
        a = list[i].getElementsByClassName("note-body")[0];
        txtValue = a.textContent || a.innerText;
        if (txtValue.toUpperCase().indexOf(filter) > -1) {
          list[i].style.display = "";
        } else {
          list[i].style.display = "none";
        }
      }
    },
  },
};
</script>

<template>
  <main>
    <div class="body">
      <DetailNote
        @show="toggleList"
        @changeTitle="changeTitle"
        @changeBody="changeBody"
        :title="notesList[noteSelected]['title']"
        :body="notesList[noteSelected]['body']"
      />
      <ListNotesVue
        v-show="showList"
        @close="toggleList"
        @add="addNote"
        @changeSelected="changeSelected"
        @search="search"
        :list="notesList"
        :noteSelected="noteSelected"
      />
    </div>
  </main>
</template>

<style>
.body {
  max-width: 1024px;
  height: 100vh;
  margin: 0 auto;
}
::-webkit-scrollbar {
  height: 6px;
  width: 6px;
  background-color: transparent;
}
::-webkit-scrollbar-thumb {
  border-radius: 3px;
  background-color: #454545;
}
::-webkit-scrollbar-track {
  border-radius: 3px;
  background-color: transparent;
}
</style>
