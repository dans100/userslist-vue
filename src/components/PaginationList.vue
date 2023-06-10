<template>
  <div>
    <button @click="previousPage" :disabled="currentPage === 1">&lt;</button>
    <button
        v-for="pageNumber in totalPages"
        :key="pageNumber"
        @click="goToPage(pageNumber)"
        :class="{ active: pageNumber === currentPage }"
    >{{ pageNumber }}</button>
    <button @click="nextPage" :disabled="currentPage === totalPages">&gt;</button>
  </div>
</template>

<script>
export default {
  props: {
    currentPage: {
      type: Number,
      required: true
    },
    totalPages: {
      type: Number,
      required: true
    }
  },

  methods: {
    previousPage() {
      if (this.currentPage > 1) {
        this.$emit('page-change', this.currentPage -1);
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.$emit('page-change', this.currentPage + 1);
      }
    },
    goToPage(pageNumber) {
      this.$emit('page-change', pageNumber);
    },
  }
}
</script>

<style scoped>

button {
  height: 40px;
  width: 40px;
  border-radius: 20px;
  cursor: pointer;
  background-color: #d7d8da;
  border: 1px solid #d9d9d9;
  color: black;
  margin: 0 5px;
}

button:hover {
  background-color: #d3d1d1;
}

button:disabled {
  cursor: not-allowed;
  opacity: 0.3;
}

.active {
  background-color: #3498db;
  border: 1px solid #3498db;
  color: white;
}

.active:hover {
  background-color: #2988c8;
}

</style>
