<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <h1>{{title}}</h1>
            
            <message v-if="message" :message='message'/>

            <newNote :note = 'note' @addNote="addNote"/>
     
            <notes :notes = 'notes'/>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import message from '@/components/Message.vue';
import notes from '@/components/Notes.vue';
import newNote from '@/components/NewNote.vue';

export default {
    components:{
        message, notes, newNote
    },
    
  data() {
    return {
      title: "Notes app",
      message: null,
      note: {
        title: "",
        descr: ""
      },
      notes: [
        {
          title: "First Note",
          descr: "Description for First Note",
          date: new Date(Date.now()).toLocaleString()
        },

        {
          title: "Second Note",
          descr: "Description for Second Note",
          date: new Date(Date.now()).toLocaleString()
        },
        {
          title: "Third Note",
          descr: "Description for Third Note",
          date: new Date(Date.now()).toLocaleString()
        }
      ]
    };
  },
  methods: {
    addNote() {
      let { title, descr } = this.note;
      if (title === "") {
        this.message = "Title can`t be empty!";
        return;
      }

      this.notes.push({
        title,
        descr,
        date: new Date(Date.now()).toLocaleString()
      });
      this.message = null;
      this.note.title = "";
      this.note.descr = "";
    }
  }
};
</script>

<style>
</style>
