<template>
  <!-- note list -->
  <div class="notes">
    <div
      class="note"
      :class="[{full: !grid}, note.status]"
      v-for="(note, index) in notes"
      :key="index"
    >
      <div class="note-header" :class="{ full: !grid }">
        <p @click="editingTitle(index)" :class="{hidden: note.editingTitle}">{{ note.title }}</p>
        <input
          class="editor"
          :class="[{active: note.editingTitle}]"
          @keyup.enter="onBlur(index)"
          @blur="onBlur(index)"
          @keyup.esc="onEsc(index)"
          type="text"
          v-model="note.title"
        />
        <p style="cursor: pointer;" @click="removeNote(index)">x</p>
      </div>
      <div class="note-body">
        <p>{{ note.descr }}</p>
        <span>{{ note.date }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    notes: {
      type: Array,
      required: true
    },
    grid: {
      type: Boolean,
      required: true
    }
  },
  methods: {
    removeNote(index) {
      this.$emit("remove", index);
    },
    editingTitle(index) {
      this.$emit("editTitle", index);
    },
    onBlur(index) {
      this.$emit("blurTitle", index);
    },
    onEsc(index) {
      this.$emit("escTitle", index);
    }
  }
};
</script>

<style lang="scss">
.notes {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 40px 0;
}
.note {
  width: 48%;
  padding: 18px 20px;
  margin-bottom: 20px;
  background-color: #ffffff;
  transition: all 0.25s cubic-bezier(0.02, 0.01, 0.47, 1);
  box-shadow: 0 10px 10px rgba(0, 0, 0, 0.2);
  &.marked {
    box-shadow: 0 10px 10px rgba(233, 213, 37, 0.2);
    &:hover {
      box-shadow: 0 20px 20px rgba(233, 213, 37, 0.1);
    }
  }
  &.important {
    box-shadow: 0 10px 10px rgba(236, 15, 15, 0.2);
    &:hover {
      box-shadow: 0 20px 20px rgba(236, 15, 15, 0.1);
    }
  }
  &:hover {
    box-shadow: 0 20px 20px rgba(0, 0, 0, 0.1);
    transform: translate(0, -6px);
    transition-delay: 0s !important;
  }
  &.full {
    width: 100%;
    text-align: center;
  }
}
.note-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: relative;
  z-index: 1;
  & .editor {
    opacity: 0;
    width: 90%;
    margin-bottom: 0;
    margin-right: 10px;
    padding: 0;
    height: 0;
    width: 0;
    border-width: 0;
    &.active {
      opacity: 1;
      padding: 16px 26px;
      height: auto;
      width: auto;
      border-width: 1px;
    }
  }
  h1 {
    font-size: 32px;
  }
  p {
    font-size: 22px;
    color: #402caf;
    &.hidden {
      display: none;
    }
  }
  svg {
    margin-right: 12px;
    color: #999999;
    &.active {
      color: #402caf;
    }
    &:last-child {
      margin-right: 0;
    }
  }
  &.full {
    justify-content: center;
    p {
      margin-right: 16px;
      &:last-child {
        margin-right: 0;
      }
    }
  }
}
.note-body {
  p {
    margin: 20px 0;
  }
  span {
    font-size: 14px;
    color: #999999;
  }
}
</style>

