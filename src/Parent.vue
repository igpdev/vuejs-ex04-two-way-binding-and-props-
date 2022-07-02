<template>
  <div id="app">
    <!-- EXERCISE 04: Two-way data binding -->
    <h1>Ex 04: Two-way Data binding</h1>
    Available users:
    <li v-for="user in users">{{ user.name }}</li>
    <br />
    <!-- Instruction 1: In the data section define a property
        called userToSearch initialized as null, and use the two-way binding
        directive to use that property in the input age tag.
    -->
    Search a user age: <input id="age" />
    <p>
      User entered <strong>{{ userToSearch }}</strong>
    </p>
    <br />
    <!-- Instruction 2: Pass the userToSearch property as a prop to the Child component. (In child component the prop has the same name 'userToSearch')-->
    <Child @fetchUsers="fetchUsersService" />
  </div>
</template>

<script>
import Child from './Child.vue';

export default {
  name: 'App',
  data: () => ({
    // Define here the property

    users: [
      { name: 'Mario', age: 29 },
      { name: 'David', age: 40 },
      { name: 'John', age: 39 },
    ],
  }),
  components: {
    Child,
  },
  methods: {
    async fetchUsersService(callback) {
      const response = await this.fakeCall();
      callback(this.users);
    },
    fakeCall() {
      return new Promise((resolve) => {
        setTimeout(function () {
          resolve();
        }, 2000);
      });
    },
  },
};
</script>

<style></style>
