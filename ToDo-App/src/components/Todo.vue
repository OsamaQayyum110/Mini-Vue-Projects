<template>
  <div class="flex justify-between items-center">
    <div>
      <input @blur="startEditing()" v-model="newData">{{ todoItem }}</input>
    </div>
    <div>
      <button @click="startEditing()"  class="bg-blue-500 px-4 py-1 m-2 rounded-lg">Edit</button>
      <button
        @click="$emit('on-delete')"
        class="bg-red-500 px-4 py-1 rounded-lg"
      >
        Delete
      </button>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    todoItem: String,
  },
  data() {
    return {
      isEditing: false,
      newData: "",
    };
  },
  methods: {
    startEditing() {
      if (!this.isEditing) {
        this.newData = this.todoItem;
        this.isEditing = true;
      } else {
        this.endEditing();
      }
    },
    endEditing() {
      this.isEditing = false;
      this.$emit("on-editing", this.newData);
    },
  },
};
</script>
