<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">

          <!-- Messages -->
          <Message v-if="message" :message="message"/>

          <!-- set priority -->
          <Priority
            :priorityItems="priorityItems"
            :checked="checked"
            @is-checked="itemChecked"
            />


          <!-- creating new note -->
          <NewNote :note="note" @addNote="addNote"/>


          <div class="note-header" style="margin: 36px 0;">
            <!-- title -->
            <h1>{{title}}</h1>

            <!-- search box -->
            <Search
              :value="search"
              placeholder="Find Your note"
              @search="search = $event"/>

            <!-- view icons -->
            <div class="icons">
              <svg :class="{active: grid}" @click="grid = true" style="cursor: pointer;" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
              <svg :class="{active: !grid}" @click="grid = false" style="cursor: pointer;" svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
            </div>
          </div>

          <!-- note list -->
          <Notes :notes="notesFilter" :grid="grid" @remove="noteRemove"/>

        </div>
      </section>
    </div>
  </div>
</template>

<script>
import Message from '@/components/Message.vue';
import NewNote from '@/components/NewNote.vue';
import Notes from '@/components/Notes.vue';
import Search from '@/components/Search.vue';
import Priority from '@/components/Priority.vue';

export default {
  components: {
    Priority,
    Search,
    Message,
    Notes,
    NewNote,

  },
  data() {
    return {
      title: "Notes app",
      search: '',
      message: null,
      grid: true,
      note: { // создаём массив заметок notes
        title: "",
        description: "",
        priority: "",
      },
      notes: [
        {
          title: "First Note",
          description: "Description for First Note",
          date: new Date(Date.now()).toLocaleString(),
          priority: 'Standart'
        },
        {
          title: "Second Note",
          description: "Description for Second Note",
          date: new Date(Date.now()).toLocaleString(),
          priority: 'Great'
        },
        {
          title: "Third Note",
          description: "Description for Third Note",
          date: new Date(Date.now()).toLocaleString(),
          priority: 'Important'
        },
      ],
      priorityItems: [
          'Standart',
          'Great',
          'Important'
      ],
      checked: 'Standart'
    };
  },
  methods: {
    // получаем переданые данные из Priority.vue и присваевем note.priority
    itemChecked (checked) {
      this.note.priority = checked
    },
    addNote() {
      let { title, description, priority } = this.note; // присвоение значение нескольким переменным
      // let noteDescriptionLength = document.querySelector(".note-description").innerHTML.length; // и так сойдёт

      if (title === "") {
        this.message = "title can`t be blank!";
        return false;
      }

      if (priority === "") {
        this.message = "set priority please";
        return false;
      }
      // if (noteDescriptionLength < 3) {
      //   this.message = "description  minimal length 3 characters ";
      //   return false;
      // }

      this.notes.push({
        title, // синтаксис ES6 позволяет опускать имя объекта, есле оно совпадает с ключом
        description,
        priority,
        date: new Date(Date.now()).toLocaleString(),
      });
      this.note.priority = "";
      this.note.title = "";
      this.note.description = "";
      this.message = null;
    },
    noteRemove(index) {
      this.notes.splice(index, 1)
    }
  },
  computed: {
    notesFilter () {
      let array = this.notes,
          search = this.search;
      if (!search) return array;
      // Small
      search = search.trim().toLowerCase();
      // Filter
      array = array.filter(function (item) {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item
        }
      });
      // Error
      return array
    }
  },
};
</script>

<style lang="scss">
  #app {
    position: relative;
  }
</style>
