<template>
  <!-- new note -->
  <div class="new-note" :class="note.status">
    <label>Title</label>
    <input v-model="note.title" type="text" />
    <label>Description</label>
    <textarea v-model="note.descr"></textarea>
    <p>choose the priority</p>
    <select v-model="note.status">
      <option v-for="(option, index) in note.options" :value="option" :key="index">{{option}}</option>
    </select>
    <button class="btn btnPrimary" @click="addNote">New note</button>
  </div>
</template>

<script>
export default {
  props: {
    note: {
      type: Object,
      required: true
    }
  },
  methods: {
    addNote() {
      this.$emit("addNote", this.note);
    }
  }
};
</script>

<style lang="scss">
.new-note {
  text-align: center;
  & select {
    display: block;
    margin: 10px auto 10px;
  }
  & p {
    margin-top: 10px;
  }
}
</style>

