<template>
  <!-- <div class="head">
    <span class="material-icons"> app_registration </span>
    <h1>Tasklist</h1>
  </div> -->
  <div class="form-container">
    <form @submit.prevent="handleSubmit">
      <label>Task</label>
      <input type="text" v-model="title" required />
      <label>Details</label>
      <textarea v-model="details" required></textarea>
      <button>Add Task</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "AddTask",
  data() {
    return {
      title: "",
      details: "",
    };
  },
  methods: {
    handleSubmit() {
      let task = {
        title: this.title,
        details: this.details,
        complete: false,
      };
      fetch("http://localhost:3000/tasks", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(task),
      })
        .then(() => {
          this.$router.push("/");
        })
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style>
/* .head {
  background-color: rgb(27, 114, 114);
  padding: 15px 0 15px 50px;
  color: white;
  display: flex;
}

.head .material-icons {
  font-size: 38px;
  padding-top: 3px;
}

.head h1 {
  margin: 0;
} */

.form-container {
  padding: 10px;
  background-color: rgba(236, 235, 235, 0.459);
  height: 90vh;
}

form {
  background-color: rgb(255, 255, 255);
  margin: 50px auto;
  width: 500px;
  border-radius: 15px;
  box-shadow: 0 3px 10px rgb(0 0 0 / 0.2);
  padding: 30px;
}

label {
  display: block;
  font-weight: bold;
  font-size: 20px;
  margin: 15px 0;
}

input {
  outline: none;
  border: none;
  width: 100%;
  font-size: 18.5px;
  font-weight: bold;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  border-bottom: 2px solid rgba(27, 114, 114, 0.513);
  padding: 5px 5px;
  color: rgb(32, 32, 32);
}

textarea {
  outline: none;
  border: none;
  font-size: 16px;
  border: 2px solid rgba(27, 114, 114, 0.527);
  width: 100%;
  height: 150px;
  color: rgb(29, 28, 28);
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-weight: 520;
  padding: 5px;
}

form button {
  display: block;
  margin: 14px auto;
  padding: 10px 15px;
  border: 0;
  background-color: rgba(27, 114, 114, 0.924);
  font-size: 16px;
  font-weight: bold;
  color: rgb(255, 240, 240);
  border-radius: 15px;
  cursor: pointer;
}
</style>
