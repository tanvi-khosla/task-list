<template>
  <div class="form-container">
    <form @submit.prevent="handleSubmit">
      <label>Task</label>
      <input type="text" v-model="title" required />
      <label>Details</label>
      <textarea v-model="details" required></textarea>
      <button>Make Changes</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "EditTask",
  props: ["id"],
  data() {
    return {
      title: "",
      details: "",
      uri: "http://localhost:3000/tasks/" + this.id,
    };
  },
  mounted() {
    fetch(this.uri)
      .then((res) => res.json())
      .then((data) => {
        this.title = data.title;
        this.details = data.details;
      });
  },
  methods: {
    handleSubmit() {
      let task = {
        title: this.title,
        details: this.details,
        complete: false,
      };
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ title: this.title, details: this.details }),
      })
        .then(() => {
          this.$router.push("/");
        })
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style></style>
