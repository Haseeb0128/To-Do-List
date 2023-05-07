<template>
  <div class="container d-flex justify-content-center">
    <div class="card mt-3 w-100">
      <div class="card-header bg-light">
        <h4>To Do List</h4>
      </div>
      <div class="card-body">
        <div class="input-container mt-3">
          <input type="text" class="form-control" name="ToDo" placeholder="What need's to be done ?" v-model="message"
            @keyup.enter="add">
        </div>
        <ul class="list-group mt-3">
          <li class="list-group-item d-flex align-items-center justify-content-between" v-for="(list, index) in lists"
            :key="list">
            <span class="message">{{ list }}</span>
            <div class="btn-group d-flex gap-3">
              <button class="btn btn-dark" @click="edit(index)">Edit</button>
              <button class="btn btn-dark" @click="remove(index)">Delete</button>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import { remove } from '@vue/shared';

export default {
  name: 'App',
  data() {
    return {
      message: "",
      editing: false,
      editingID: 0,
      lists: ["Research Vue JS", "Learn Vue JS", "Implement Vue JS"],
    }
  },

  methods: {
    add: function () {
      if (this.message !== "") {
        if (this.editing) {
          this.lists[this.editingID] = this.message;
          this.message = "";
          this.editing = false;
        }
        else {
          this.lists.push(this.message);
          this.message = "";
        }
      }
    },
    remove: function (index) {
      this.lists.splice(index, 1);
    },
    edit: function (index) {
      this.message = this.lists[index];
      this.editing = true;
      this.editingID = index;
    }
  }
}
</script>