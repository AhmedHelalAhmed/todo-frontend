<template>
<div class="container">
  <div
    v-if="submitted"
    class="alert alert-success"
    role="alert">
      A Task added successfully
  </div>
  <form v-on:submit.prevent>
    <div class="form-group">
      <div class="input-group mb-3">
        <input
          placeholder="enter a task"
          v-on:keyup.enter="addtask"
          v-model='description'
          type="text"
          class="form-control"
          aria-label="task's description"
        aria-describedby="basic-addon2">
        <div class="input-group-append">
          <button
            class="btn btn-primary"
            type="button"
            v-on:click="addtask">
            Add task
        </button>
        </div>
      </div>
    </div>
  </form>
</div>
</template>
<script>
export default {
  data() {
    return {
      submitted: false,
      description: "",
    }
  },

  methods: {
    addtask()
    {
      /*
        event from child to parent to change it's value
        and set it with new value that is entered
      */
      //add to backend
      this.$http.post("api/tasks", {

        description: this.description

      }, {

        emulateJSON: true

      }).then(response => {

        // console.log(response.data);

        //reset the description
        this.description = "";

        //add to frontend
        this.$emit('addTask', response.data);
      });

    },
  },

}
</script>
<style>
</style>
