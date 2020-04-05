<template>
  <div class="note_new">
    <label>Title</label>
    <input type="text" v-model="note.title" />

    <div class="priority">
      <p>
        <input
          class="radio"
          value="Standard"
          type="radio"
          id="standard"
          name="radio-group"
          v-model="note.priority"
        />
        <label class="priority_standard" for="standard">Standard</label>
      </p>
      <p>
        <input
          class="radio"
          type="radio"
          value="Important"
          id="important"
          name="radio-group"
          v-model="note.priority"
        />
        <label class="priority_important" for="important">Important</label>
      </p>
      <p>
        <input
          class="radio"
          type="radio"
          id="v-important"
          value="Very Important"
          name="radio-group"
          v-model="note.priority"
        />
        <label class="priority_v-important" for="v-important">Very important</label>
      </p>
    </div>

    <label>Descriptiond</label>
    <textarea v-model="note.descr"></textarea>
    <button class="btn btnPrimary" @click="addNote">Add Note</button>
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
<style lang="scss" scoped>
button {
  margin-top: 20px;
}
.note_new {
  text-align: center;
}
.priority {
  display: flex;
  width: 100%;
  align-items: center;
  justify-content: space-between;
  & p {
    font-size: 18px;
  }
}

// Radio button
.radio:checked,
.radio:not(:checked) {
  position: absolute;
  left: -9999px;
}
.radio:checked + label,
.radio:not(:checked) + label {
  position: relative;
  padding-left: 28px;
  cursor: pointer;
  line-height: 20px;
  display: inline-block;
  color: #666;
}
.radio:checked + label:before,
.radio:not(:checked) + label:before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  width: 20px;
  height: 20px;
  border: 1px solid #ddd;
  border-radius: 100%;
  background: #fff;
}
.radio:checked + label:after,
.radio:not(:checked) + label:after {
  content: "";
  width: 12px;
  height: 12px;
  background: gray;
  position: absolute;
  top: 4px;
  left: 4px;
  border-radius: 100%;
  -webkit-transition: all 0.2s ease;
  transition: all 0.2s ease;
}
.radio:checked + .priority_standard:after,
.radio:not(:checked) + .priority_standard:after {
  background-color: green;
}
.radio:checked + .priority_important:after,
.radio:not(:checked) + .priority_important:after {
  background-color: orange;
}
.radio:checked + .priority_v-important:after,
.radio:not(:checked) + .priority_v-important:after {
  background-color: red;
}
.radio:not(:checked) + label:after {
  opacity: 0;
  -webkit-transform: scale(0);
  transform: scale(0);
}
.radio:checked + label:after {
  opacity: 1;
  -webkit-transform: scale(1);
  transform: scale(1);
}
</style>