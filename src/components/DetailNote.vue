<script>
import ListNotesVue from "./ListNotes.vue";

export default {
  name: "DetailNote",
  methods: {
    toggleList() {
      this.$emit("show");
    },
    changeTitle() {
      var title = document.getElementsByClassName("input-title")[0].value;
      this.$emit("changeTitle", title);
    },
    changeBody() {
      var body = document.getElementsByClassName("input-body")[0].value;
      this.$emit("changeBody", body);
    },
  },
  props: ["title", "body"],
};
</script>

<template>
  <div class="detail-container">
    <div class="head">
      <div class="head-text" @click="toggleList">&lt; Notes</div>
    </div>
    <div class="content">
      <input
        type="text"
        class="input input-title"
        placeholder="Title"
        :value="title"
        @change="changeTitle"
      />
      <textarea
        type="text"
        class="input input-body"
        placeholder="Body"
        :value="body"
        @change="changeBody"
      />
    </div>
  </div>
</template>

<style scoped>
.detail-container {
  background-color: black;
  padding: 8px;
  height: 100vh;
}

.head {
  height: 40px;
  padding: 8px;
}
.head-text {
  color: #ffd52e;
  font-weight: 700;
  font-size: 17px;
  cursor: pointer;
}
.content {
  background-color: #141414;
  border-radius: 8px;
  height: calc(100% - 48px);
}
.input {
  width: 100%;
  background: none;
  border: none;
  color: #fff;
  padding: 10px;
}
.input:focus {
  outline: none;
}
.input-title {
  font-weight: 500;
  font-size: 25px;
  border-bottom: solid 1px rgba(255, 255, 255, 0.2);
  height: 50px;
}
.input-body {
  width: 100%;
  height: calc(100% - 98px);
}
</style>
