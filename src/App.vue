<template>
<div class="wrapper">

  <div class="wrapper-content">
    <section>
      <div class="container">
        <!-- message -->
        <message v-if="message" :message="message"/>
        <!-- new note -->
        <newNote
            :note="note"
            @addNote="addNote"/>
        <div class="note__header" style="margin: 36px 0">
             <!-- title -->
            <h1>{{ title }}</h1>
            <search :value="search" placeholder="Поиск заметок" @search ="search = $event"/>
            <div class="icons">
                <svg :class="{ active: grid }" @click="grid = true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
                <svg :class="{ active: !grid }" @click="grid = false" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>

            </div>
        </div>
            <!-- note list -->
        <notes
        :notes="notesFilter"
        @remove="removeNote"
        :grid="grid"
        />
      </div>
    </section>

  </div>

  <!-- footer -->
  </div>
</template>

<script>
import message from "@/components/Message.vue";
import Message from './components/Message.vue';
import newNote from './components/NewNote.vue';
import notes from './components/Notes.vue';
import search from './components/Search.vue';
export default {
  components: {
        message, newNote, notes,search

    },
  data () {
    return {
                title: 'Приложение "Заметки"',
                search: '',

                message: null,
                grid: true,
                note: {
                    title: '',
                    descr: ''
                },
                notes: [
                    {
                        title: 'Первая заметка',
                        descr: 'Описание первой заметки',
                        date: new Date(Date.now()).toLocaleString()
                    },
                    {
                        title: 'Вторая заметка',
                        descr: 'Описание второй заметки',
                        date: new Date(Date.now()).toLocaleString()
                    },
                    {
                        title: 'Третья заметка',
                        descr: 'Описание третьей заметки',
                        date: new Date(Date.now()).toLocaleString()
                    },
                ]

    }

  },
  computed: {
    notesFilter () {
      let array = this.notes,
          search = this.search
      if (!search) return array
      // Small
      search = search.trim().toLowerCase()
      // Filter
      array = array.filter(function (item) {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item
        }
      })
      // Error
      return array
    }
  },
   methods: {
                addNote() {
                    // let {title, descr} = this.note
                    if(this.note.title === '') {
                        this.message = 'Название заметки не может быть пустым!'
                        return false
                    }
                    if(this.note.descr === '') {
                        this.message = 'Описание не может быть пустым!'
                        return false
                    }
                    this.notes.push({
                        title: this.note.title,
                        descr: this.note.descr,
                        date:  new Date(Date.now()).toLocaleString()
                    })
                    this.note.title = ''
                    this.note.descr = ''
                    this.message = null
                },

                removeNote (index) {
                    this.notes.splice(index, 1)

                }

            }

}
</script>

<style>

</style>
