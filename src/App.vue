<template>
  <div class="container w-50 my-5 shadow p-4">
    <h3 class="text-center mb-5">Vue Todo App</h3>
    <form @submit.prevent="addTask()" class="d-flex justify-content-center">
      <div class="">
        <input
          type="text"
          class="form-control"
          id="exampleFormControlInput1"
          placeholder="Add item"
          v-model="item"
          required
        />
      </div>
      <button type="submit" class="btn btn-primary btn-sm">Add</button>
    </form>

    <div class="result mt-5">
      <div class="d-flex justify-content-between align-items-center mb-4">
        <h5>Your Task</h5>
        <div>
          <input
            type="text"
            v-model="search"
            class="form-control"
            placeholder="Search"
          />
        </div>
      </div>
      <div
        class="position-relative w-100 py-1"
        v-for="(task, index) in searchTask"
        :key="index"
      >
        <input
          type="checkbox"
          v-model="task.isComplete"
          :value="(isComplete = true)"
        />
        <span class="mx-1" :class="{ 'line-through': task.isComplete }">{{
          task.value
        }}</span>
        <span
          class="float-end text-danger"
          style="cursor: pointer"
          @click="removetask(index)"
          >Remove</span
        >
      </div>
      <div class="border-0" v-if="tasks.length === 0">
        <p class="text-danger">No Task found</p>
      </div>
    </div>
    <button class="btn btn-danger btn-sm d-block mt-4" @click="removeAll()">
      Clear Task
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [],
      item: "",
      search: "",
    };
  },
  methods: {
    addTask() {
      this.tasks.push({
        value: this.item,
        isComplete: false,
      });
      this.item = "";
    },
    removetask(index) {
      this.tasks.splice(index, 1);
    },
    removeAll() {
      this.tasks = [];
    },
  },
  computed: {
    searchTask() {
      if (this.search) {
        return this.tasks.filter(
          (task) => task.value.indexOf(this.search) !== -1
        );
      } else {
        return this.tasks;
      }
    },
  },
};
</script>

<style scoped>
.line-through {
  text-decoration: line-through;
}
</style>
