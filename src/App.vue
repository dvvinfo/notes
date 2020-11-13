<template>
<div class="wrapper">
  <!-- header -->
  <div class="wrapper-content">
    <section>
      <div class="container">
        <h1>{{ title }}</h1>
        <message v-if="message" :message="message"/>
        <newNote
            :note="note"
            @addNote="addNote"/>
        
        <notes
        :notes="notes"/>
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

export default {
  components: {
        message, newNote, notes

    },
  data () {
    return {
      title: 'Приложение "Заметки"',
                message: null,
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
                }
            }

}
</script>

<style>

</style>
