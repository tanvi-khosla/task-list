<template>
  <div class="home">
    <Filter
      @filterChange="currentFilter = $event"
      :currentFilter="currentFilter"
    />
    <div v-if="tasks.length">
      <div v-for="task in filteredTasks" :key="task.id">
        <SingleTask
          :task="task"
          @delete="handleDelete"
          @complete="handleComplete"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SingleTask from "../components/SingleTask.vue";
import Filter from "../components/Filter.vue";

export default {
  name: "Home",
  components: { SingleTask, Filter },
  data() {
    return {
      tasks: [],
      currentFilter: "all",
    };
  },
  mounted() {
    fetch("http://localhost:3000/tasks")
      .then((res) => res.json())
      .then((data) => (this.tasks = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    handleDelete(id) {
      this.tasks = this.tasks.filter((task) => {
        return task.id !== id;
      });
    },
    handleComplete(id) {
      let t = this.tasks.find((task) => {
        return task.id === id;
      });
      t.complete = !t.complete;
    },
  },
  computed: {
    filteredTasks() {
      if (this.currentFilter === "completed") {
        return this.tasks.filter((task) => task.complete);
      }
      if (this.currentFilter === "ongoing") {
        return this.tasks.filter((task) => !task.complete);
      }
      return this.tasks;
    },
  },
};
</script>

<style>
.home {
  padding: 30px 50px;
  background-color: rgba(236, 235, 235, 0.459);
  height: 90vh;
}
</style>
