<template>
  <div class="notes">
    <div class="note" v-for="(note,index) in notes" :key="index">
      <div class="note__header">
        <p>{{note.title}}</p>
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
.note{
    width: 48%;
    padding: 18px 20px;
    margin-bottom: 20px;
    background-color: white;
}
.note__header{
    p{
        font-size: 22px;
        color: #203fa5;
    }
}
.note__body{
    p{
        margin: 20px 0;
    }
    span{
        font-size: 14px;
        color: #999999;
    }
}
</style>