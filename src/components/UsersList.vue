<template>
  <div class="container">
    <ul>
    <li v-for="user in paginatedUsers" :key="user.id">
      <img :src="user.picture.medium"/>
          <strong>{{user.name.first}} {{user.name.last}}</strong>
    </li>
    </ul>
    <pagination-list
      :current-page="currentPage"
      :total-pages="totalPages"
      @page-change="changePage"
    ></pagination-list>
  </div>
</template>

<script>
import axios from 'axios';
import PaginationList from "@/components/PaginationList";


export default {
  components: {PaginationList},
  data() {
    return {
      users: [],
      currentPage: 1,
      usersPerPage: 10,
    }
  },

  async mounted() {
    await this.getUsers();
  },

  computed: {
    totalPages() {
      return Math.ceil(this.users.length / this.usersPerPage);
    },
    paginatedUsers() {
     const startIndex = (this.currentPage - 1) * this.usersPerPage;
     const endIndex = startIndex + this.usersPerPage;
     return this.users.slice(startIndex, endIndex);
    }
  },

  methods: {
    async getUsers() {
      try {
        const response = await axios.get('https://randomuser.me/api/?results=50');
        this.users = response.data.results;
      } catch (e) {
        console.error(e);
      }
    },
    changePage(pageNumber) {
      this.currentPage = pageNumber;
    }
  }
}

</script>

<style scoped>

.container {
  margin: 0 auto;
  width: 600px;
  height: auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #b8babe;
  border-radius: 10px;
  padding: 30px 0 30px 0;
  box-shadow: 2px 2px 2px #b8babe;
}

ul {
  list-style: none;
  width: 80%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 0;
  visibility: hidden;
}

ul > * {
  visibility: visible;
  transition: opacity 0.5s ease;
}

ul:hover > :not(:hover) {
  opacity: 0.3;
}

li {
  width: 70%;
  padding: 10px;
  display: flex;
  align-items: center;
  background-color: #d7d8da;
  border: 1px solid #b8babe;
  border-radius: 5px;
  cursor: pointer;
}

img {
  width: 50px;
  height: auto;
  border-radius: 50%;
  margin-right: 20px;
}

</style>
