<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <message v-if="message" :message="message" />

          <newNote :note="note" @addNote="addNote" />
          <div class="note__header">
            <h1>{{title}}</h1>
            <search :value="search" placeholder="Find your note" @search="search = $event" />
            <div class="icons">
              <svg
                :class="{active : grid}"
                @click="grid = true"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <rect x="3" y="3" width="7" height="7" />
                <rect x="14" y="3" width="7" height="7" />
                <rect x="14" y="14" width="7" height="7" />
                <rect x="3" y="14" width="7" height="7" />
              </svg>
              <svg
                :class="{active : !grid}"
                @click="grid = false"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <line x1="8" y1="6" x2="21" y2="6" />
                <line x1="8" y1="12" x2="21" y2="12" />
                <line x1="8" y1="18" x2="21" y2="18" />
                <line x1="3" y1="6" x2="3" y2="6" />
                <line x1="3" y1="12" x2="3" y2="12" />
                <line x1="3" y1="18" x2="3" y2="18" />
              </svg>
            </div>
          </div>

          <notes :notes="notesFilter" :grid="grid" @remove="removeNote" @change="changeTitle" />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import message from "@/components/Message.vue";
import notes from "@/components/Notes.vue";
import newNote from "@/components/NewNote.vue";
import search from "@/components/Search.vue";

export default {
  components: {
    message,
    notes,
    newNote,
    search
  },

  data() {
    return {
      title: "Notes app",
      message: null,
      grid: true,
      search: "",
      note: {
        title: "",
        descr: "",
        priority: "Standard"
      },
      notes: [
        {
          title: "First Note",
          descr: "Description for First Note",
          date: new Date(Date.now()).toLocaleString(),
          priority: "Standard"
        },

        {
          title: "Second Note",
          descr: "Description for Second Note",
          date: new Date(Date.now()).toLocaleString(),
          priority: "Standard"
        },
        {
          title: "Third Note",
          descr: "Description for Third Note",
          date: new Date(Date.now()).toLocaleString(),
          priority: "Standard"
        }
      ]
    };
  },
  computed: {
    notesFilter() {
      let array = this.notes,
        search = this.search;
      if (!search) {
        return array;
      }
      search = search.trim().toLowerCase();

      array = array.filter(function(item) {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item;
        }
      });
      // Error
      return array;
    }
  },
  methods: {
    addNote() {
      let { title, descr, priority } = this.note;
      if (title === "") {
        this.message = "Title can`t be empty!";
        return;
      }

      this.notes.push({
        title,
        descr,
        priority,
        date: new Date(Date.now()).toLocaleString()
      });
      this.message = null;
      this.note.title = "";
      this.note.descr = "";
      this.note.priority = "Standard";
    },
    removeNote(index) {
      this.notes.splice(index, 1);
    },
    changeTitle(index) {
      let note = this.notes.find(function(item, indexNote) {
        if (indexNote === index) {
          return item;
        }
      });
      note.editing = true;

      console.log(note);
    }
  }
};
</script>

<style>
</style>
