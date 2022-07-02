<template>
  <div>
    <button @click="emitFetchUsersEvent">Search user info</button>
    <p v-if="loading">Searching age of user selected...</p>
    <br></br>
    <span v-if="user"><strong>
      {{ user.name }} has {{ user.age }} years.
    </strong></span>
  </div>
</template>

<script>
export default {
  name: 'Child',
  props: {
    userToSearch: {
      type: String
    }
  },
  data() {
    return {
      loading: false,
      user: null
    };
  },
  methods: {
    emitFetchUsersEvent() {
      this.loading = true;
      this.user = null;
      
      this.$emit
      ('fetchUsers', (res) => {
        this.user = null,
        this.loading = false;
        this.user = res.filter((user) => 
          user.name.toLowerCase().includes(this.userToSearch.toLowerCase())
        )[0]
      });
    },
  }
};
</script>

<style>
div {
  display: grid;
  place-items: center;
}
</style>
