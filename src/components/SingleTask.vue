<template>
  <div class="task" :class="{ complete: task.complete }">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ task.title }}</h3>
    </div>
    <div v-if="showDetails" class="details">
      <span class="task-details">{{ task.details }}</span>
      <div class="edit-del-done">
        <router-link
          style="text-decoration: none; color: inherit"
          :to="{ name: 'EditTask', params: { id: task.id } }"
        >
          <span @click="editTask" class="material-icons"> edit </span>
        </router-link>
        <span @click="deleteTask" class="material-icons"> delete </span>
        <span @click="toggleComplete" class="material-icons tick"> done </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["task"],
  data() {
    return {
      showDetails: false,
      uri: "http://localhost:3000/tasks/" + this.task.id,
    };
  },
  methods: {
    deleteTask() {
      fetch(this.uri, { method: "DELETE" })
        .then(() => this.$emit("delete", this.task.id))
        .catch((err) => console.log(err.message));
    },
    toggleComplete() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ complete: !this.task.complete }),
      })
        .then(() => {
          this.$emit("complete", this.task.id);
        })
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style>
.task {
  background-color: rgb(255, 255, 255);
  padding: 5px 25px;
  margin: 30px auto;
  border-radius: 15px;
  box-shadow: 0 3px 10px rgb(0 0 0 / 0.2);
  border-left: 15px solid rgba(231, 96, 96, 0.746);
  width: 600px;
}

.task.complete {
  border-left: 15px solid rgba(36, 144, 112, 0.534);
}

.task.complete .tick {
  color: rgba(36, 144, 112, 0.534);
}

.actions {
  display: flex;
  justify-content: space-between;
}

.actions h3 {
  cursor: pointer;
}

.details {
  display: flex;
  justify-content: space-between;
}

.task-details {
  padding: 20px 0;
}

.edit-del-done .material-icons {
  font-size: 20px;
  padding: 20px 7px 0 7px;
  color: rgb(133, 133, 133);
  cursor: pointer;
}

.edit-del-done .material-icons:hover {
  color: rgb(75, 74, 74);
}
</style>
