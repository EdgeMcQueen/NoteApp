<template>
    <!-- new note -->
    <div class="new-note">
        <label for="note-title">Title</label>
        <input v-model="note.title" type="text" id="note-title"/>
        <label for="note-description">Description</label>
        <textarea v-model="note.description" class="note-description" id="note-description"></textarea>
        <button class="btn btnPrimary" @click="addNote">New note</button>
    </div>
</template>

<script>
export default {
    props: {
        note: {
            type: Object,
            required: true
        },
    },
    data() {
        return {

        }
    },
    methods: {
        addNote () {
            this.$emit('addNote', this.note);
        },
    },
}
</script>

<style lang="scss">
    .new-note {
        position: relative;
        text-align: center;
        .btn {
            margin: 20px 0;
        }
    }
</style>