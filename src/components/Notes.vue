<template>
  <div class="notes">
    <note v-for="(note,index) in notes" :key="index" :note="note" :grid="grid" @remove="removeNote"/>
  </div>
</template>
<script>
import note from "@/components/Note.vue";

export default {
  components: {
    note
  },
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
</style>