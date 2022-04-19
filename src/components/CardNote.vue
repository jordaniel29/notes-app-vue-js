<script setup>
defineProps({
  title: {
    type: String,
    required: true,
  },
  body: {
    type: String,
    required: true,
  },
  date: {
    type: String,
    required: true,
  },
  selected: {
    type: Boolean,
    required: true,
  },
  first: {
    type: Boolean,
  },
  last: {
    type: Boolean,
  },
});
</script>

<template>
  <div
    class="card-note"
    :class="[{ active: selected }, { last: last }, { first: first }]"
  >
    <div class="note-title">{{ title }}</div>
    <div class="note-body">{{ body }}</div>
    <div class="note-date">{{ date }}</div>
  </div>
</template>

<style scoped>
.card-note {
  width: 100%;
  height: 101px;
  padding: 8px;
  cursor: pointer;
  border-bottom: solid 1px rgba(255, 255, 255, 0.2);
}
.first {
  border-radius: 5px 5px 0 0;
}
.active {
  background-color: #ffd52e;
}
.last {
  border: none;
  border-radius: 0 0 5px 5px;
}
.note-title {
  font-size: 18px;
  font-weight: bolder;
  margin-bottom: 5px;
  height: 29px;
}
.note-body {
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
  margin-bottom: 5px;
  color: #ffffffe6;
  height: 26px;
}
.note-date {
  text-align: right;
  font-size: 12px;
  font-weight: bolder;
  color: #ffffffe6;
  height: 19px;
}
</style>
