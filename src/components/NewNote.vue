<template>
    <!-- new note -->
        <div class="new-note">
            <label> Название заметки</label>
            <input type="text" v-model="note.title">
            <label >Описание</label>
            <textarea v-model="note.descr"></textarea>
            <button @click="addNote" class="btn btnPrimary">Добавить заметку</button>
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
            this.$emit('addNote', this.note)
        }
    }
}
</script>
<style lang="scss">
.new-note {
    text-align: center;
}
.btn{
    margin-top: 20px;
}

</style>