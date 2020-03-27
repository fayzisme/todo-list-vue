<template>
  <article class="message">
    <div class="message-header">
      <p>{{ note.title }}</p>
      <button @click="deleteNote" class="delete" aria-label="delete"></button>
    </div>
    <div class="message-body">
      <UpdateNoteModal :note="note" @updateNote="updateNote" :key="note._id" />
    </div>
  </article>
</template>
<script>
import { deleteNote } from "../repository";
import UpdateNoteModal from "./UpdateNoteModal";
export default {
  name: "NoteItem",
  props: ["note"],
  components: { UpdateNoteModal },
  methods: {
    deleteNote(e) {
      e.preventDefault();
      deleteNote(this.note._id)
        .then(() => this.$emit("deleteNote", this.note._id))
        .catch(err => alert(err));
    },
    updateNote(note) {
      this.$emit("updateNote", note);
    }
  }
};
</script>