<template>
  <h1>Lista użytkowników</h1>
  <div>
    <ul>
    <li v-for="user in users" :key="user.id">
      <img :src="user.picture.medium"/>
          {{user.name.first}} {{user.name.last}}
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


