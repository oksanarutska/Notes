<template>
        <div class="note_new">
            <label>Title</label>
            <input type="text" v-model="note.title" />
             <label>Descriptiond</label>
            <textarea v-model="note.descr"></textarea>
            <button class="btn btnPrimary" @click="addNote">Add Note</button>
          </div>
    
</template>
<script>
export default {
    props:{
        note:{
            type: Object,
            required: true
        }

    }, 
    
    methods:{
        addNote(){
            this.$emit('addNote', this.note)
        }
    }
    
}
</script>
<style lang="scss" scoped>
button{
    margin-top: 20px;
}
 .note_new{
     text-align: center;
 }
</style>