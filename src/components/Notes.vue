<template>
  <div class="notes">
    <div class="note" :class="{full : !grid}" v-for="(note,index) in notes" :key="index">
      <div class="note__header">
        <p>{{note.title}}</p>
        <p style="cursor:pointer" @click="removeNote(index)">X</p>
      </div>
      <div class="note__body">
        <p>{{note.descr}}</p>
        <p>{{note.date}}</p>
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
  background-color: white;
  transition: all 0.25s cubic-bezier(0.02, 0.01, 0.47, 1);
  box-shadow: 0 30px 30px rgba(0, 0, 0, 0.2);
  &:hover{
      box-shadow: 0 30px 30px rgba(0, 0, 0, 0.4);
      transform: translate(0, -6px);
      transition-delay: 0s!important;
  }
  &.full{
    width: 100%;
    text-align: center;
  }
}
.note__header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 36px 0;
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
    &.active{
      color: #203fa5;
    }
  }
   &.full {
     justify-content: center;
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
</style>