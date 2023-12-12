<template>
  <div>
    <button @click="confirmInput">Confirm</button>
    <button @click="saveChanges">Save</button>
    <ul>
      <user-item
        v-for="user in users"
        :key="user.id"
        :name="user.fullName"
        :role="user.role"
      ></user-item>
    </ul>
  </div>
</template>

<script>
import UserItem from './UserItem.vue';

export default {
  components: {
    UserItem,
  },
  data() {
    return {
      changesSaved: false,
    };
  },
  inject: ['users'],
  methods: {
    confirmInput() {
      this.$router.push('/teams');
    },
    saveChanges() {
      this.changesSaved = true;
    },
  },

  beforeRouteLeave(to, from, next) {
    console.log('UsersList component before route lift');
    console.log(from, to);
    if (this.changesSaved) {
      next();
    }else{
       const userWantToLeavePrompt = confirm('are you sure?')
       next(userWantToLeavePrompt)
    }
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 2rem auto;
  max-width: 20rem;
  padding: 0;
}
</style>
