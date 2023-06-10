<template>
  <h1>Lista użytkowników</h1>
  <div>
    <ul>
    <li v-for="user in users" :key="user.id">
      <img :src="user.picture.medium"/>
          <strong>{{user.name.first}} {{user.name.last}}</strong>
    </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';


export default {
  data() {
    return {
      users: []
    }
  },

  async mounted() {
    await this.fetchUsers();
  },

  methods: {
    async fetchUsers() {
      try {
        const response = await axios.get('https://randomuser.me/api/?results=50');
        this.users=response.data.results;
      } catch (e) {
        console.error(e);
      }
    }
  }
}

</script>

<style scoped>

h1 {
  text-align: center;
  text-transform: uppercase;
  font-weight: 300;
  letter-spacing: 2px;
}

div {
  margin: 0 auto;
  width: 600px;
  height: auto;
  display: flex;
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
