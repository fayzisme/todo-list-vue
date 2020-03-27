<template>
  <div>
    <div class="modal" :class="{ 'is-active': isActive }">
      <div class="modal-background"></div>
      <div class="modal-card">
        <header class="modal-card-head">Update Note</header>
        <section class="modal-card-body">
          <div class="field">
            <div class="control">
              <input v-model="title" class="input" type="text" placeholder="title" />
            </div>
          </div>
          <button @click="update" class="button is-primary is-pulled-right">Add</button>
        </section>
      </div>
      <button @click="toggle" class="modal-close is-large" aria-label="close"></button>
    </div>
    <button @click="toggle" class="button is-small is-pulled-right">Edit</button>
  </div>
</template>
<script>
import { updateNote } from "../repository";
export default {
  name: "UpdateNoteModal",
  data() {
    return {
      title: this.note.title,
      isActive: false
    };
  },
  props: ["note"],
  methods: {
    update() {
      let data = { title: this.title };
      updateNote(data, this.note._id)
        .then(data => {
          this.$emit("updateNote", data.note);
          this.toggle();
        })
        .catch(err => alert(err.message));
    },
    toggle() {
      this.isActive = !this.isActive;
    }
  }
};
</script>