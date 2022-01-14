<template>
  <div class="filter">
    <button
      @click="updateFilter('all')"
      :class="{ active: currentFilter === 'all' }"
    >
      All Tasks
    </button>
    <button
      @click="updateFilter('completed')"
      :class="{ active: currentFilter === 'completed' }"
    >
      Completed Tasks
    </button>
    <button
      @click="updateFilter('ongoing')"
      :class="{ active: currentFilter === 'ongoing' }"
    >
      Ongoing Tasks
    </button>
  </div>
</template>

<script>
export default {
  props: ["currentFilter"],
  methods: {
    updateFilter(by) {
      this.$emit("filterChange", by);
    },
  },
};
</script>

<style>
.filter {
  margin: 0 350px;
  display: flex;
  justify-content: space-between;
}
.filter button {
  border: none;
  background-color: transparent;
  font-size: 14px;
  color: rgb(173, 173, 173);
  font-weight: 580;
  text-transform: uppercase;
  cursor: pointer;
}
.filter button:hover {
  color: rgb(27, 93, 88);
}
.filter button.active {
  color: rgb(27, 93, 88);
}
</style>
