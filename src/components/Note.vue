<template>
  <div class="note" :class="{full : !grid}">
    <div class="note__header">
      <p v-if="!editing" class="note__title" @click="changeEdit">{{note.title}}</p>
      <div class="note__title-change" v-if="editing">
        <input  v-model="title" />
        <svg
          class="button-submit"
          @click="submit"
          xmlns="http://www.w3.org/2000/svg"
          height="24"
          viewBox="0 0 24 24"
          width="24"
        >
          <path d="M0 0h24v24H0z" fill="none" />
          <path d="M9 16.2L4.8 12l-1.4 1.4L9 19 21 7l-1.4-1.4L9 16.2z" />
        </svg>

        <svg
          class="button-close"
          @click="close"
          xmlns="http://www.w3.org/2000/svg"
          height="24"
          viewBox="0 0 24 24"
          width="24"
        >
          <path
            d="M19 6.41L17.59 5 12 10.59 6.41 5 5 6.41 10.59 12 5 17.59 6.41 19 12 13.41 17.59 19 19 17.59 13.41 12z"
          />
          <path d="M0 0h24v24H0z" fill="none" />
        </svg>
      </div>

      <p style="cursor:pointer" @click="remove">X</p>
    </div>
    <div class="note__body">
      <p class="note__descr">{{note.descr}}</p>
      <p>{{note.date}}</p>
      <p
        class="priority"
        :class="{
          standard: note.priority === 'Standard',
          important: note.priority === 'Important',
          vImportant: note.priority === 'Very Important'

          }"
      >
        <span></span>
        {{note.priority}}
      </p>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      editing: false,
      title: this.note.title
    };
  },
  props: {
    note: {
      type: Object,
      required: true
    },
    grid: {
      type: Boolean,
      required: true
    }
  },
  methods: {
    changeEdit() {
      this.editing = true;
    },
    close() {
      this.editing = false;
      this.title = this.note.title;
    },
    submit() {
      this.editing = false;
      this.note.title = this.title;
      this.note.date = new Date(Date.now()).toLocaleString()
    },
    remove(){
        this.$emit('remove')
    }
  }
};
</script>

<style lang="scss">
.note {
  width: 48%;
  height: 300px;
  padding: 18px 20px;
  margin-bottom: 20px;
  overflow: hidden;
  background-color: white;
  transition: all 0.25s cubic-bezier(0.02, 0.01, 0.47, 1);
  box-shadow: 0 30px 30px rgba(0, 0, 0, 0.2);
  &:hover {
    box-shadow: 0 30px 30px rgba(0, 0, 0, 0.4);
    transform: translate(0, -6px);
    transition-delay: 0s !important;
  }
  &.full {
    width: 100%;
    text-align: center;
  }
}

.note__header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 10px 0;
  h1 {
    font-size: 32px;
  }
  p {
    font-size: 22px;
    color: #203fa5;
  }
  svg {
    color: grey;
    cursor: pointer;
    &:not(:last-child) {
      margin-right: 10px;
    }
    &.active {
      color: #203fa5;
    }
  }
  &.full {
    justify-content: center;
  }
}
.note__title {
  &:hover {
    cursor: url("../assets/cursor.svg") 10 10, pointer;
  }
}
.note__body {
  p {
    margin: 20px 0;
  }
  span {
    font-size: 14px;
    color: #999999;
  }
}
.priority {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  & span {
    display: block;
    margin-right: 10px;
    width: 20px;
    height: 20px;
    border-radius: 100%;
    background-color: gray;
  }
  &.standard {
    & span {
      background-color: green;
    }
  }
  &.important {
    & span {
      background-color: orange;
    }
  }
  &.vImportant {
    & span {
      background-color: red;
    }
  }
}
.note__descr {
  height: 100px;
  overflow: auto;
  &::-webkit-scrollbar {
    display: none;
  }
}
.note__title-change {
  position: relative;
  width: 80%;
  & input{
      margin-bottom: 0;
  }
  & svg {
    position: absolute;
    top: 15px;
    right: 35px;
    cursor: pointer;
    transition: all 0.2s ease-in-out;
    &:hover {
      fill: gray;
    }
    &:last-child {
      right: 5px;
    }
  }
}
</style>