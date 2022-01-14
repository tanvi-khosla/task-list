<template>
  <div class="head">
    <div class="branding">
      <span class="material-icons"> app_registration </span>
      <router-link
        style="text-decoration: none; color: inherit"
        :to="{ name: 'Home' }"
      >
        <h1>Tasklist</h1>
      </router-link>
    </div>
    <div class="add-btn">
      <router-link
        style="text-decoration: none; color: inherit"
        :to="{ name: 'AddTask' }"
        ><span class="material-icons"> add_circle </span></router-link
      >
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style>
.head {
  background-color: rgb(27, 114, 114);
  padding: 5px 70px 5px 70px;
  color: white;
  display: flex;
  justify-content: space-between;
}

.branding {
  display: flex;
}

.branding .material-icons {
  padding: 25px 0 0 0;
  font-size: 35px;
}

.add-btn .material-icons {
  padding: 25px 0 0 0;
  font-size: 30px;
  cursor: pointer;
}
</style>
