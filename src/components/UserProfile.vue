<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">
          Admin
      </div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ followers }}
      </div>
      <form class="user-profile__create-twoot">
        <label for="newTwoot"><strong>New Twoot</strong></label>
        <textarea id="newTwoot" rows="4"></textarea>
      </form>
    </div>
    <div class="user-profile__twoots-wrapper">
        <TwootItem 
          v-for="twoot in user.twoots" 
          :key="twoot.id" 
          :username="user.username" 
          :twoot="twoot" 
          @favourite = "toggleFavourite"
        />
    </div>
  </div>
</template>

<script>
import TwootItem from './TwootItem'

export default {
  name: 'UserProfile',
  components: {TwootItem},
  data() {
    return{
      followers: 0,
      user: {
        id: 1,
        username: 'arnavdixit',
        firstName: 'Arnav',
        lastName: 'Dixit',
        email: 'abc@gmail.com',
        isAdmin: true,
        twoots: [
            {id:1, content: 'Twotter is amazing'},
            {id:2, content: 'Earth is amazing!'}
        ]
      }
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount){
      if(oldFollowerCount<newFollowerCount){
        console.log(`${this.user.username} has gained a follower!`);
      }
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    }
  },
  methods: {
    followUsers() {
      this.followers++;
    },
    toggleFavourite(id){
      console.log(`Favourited Twoot #${id}`);
    }
  },
  mounted () {
    this.followUsers();
  }
}
</script>

<style>
.user-profile{
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;
}

.user-profile__user-panel{
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
    text-align: left;
}

.user-profile__admin-badge{
    background-color:rebeccapurple;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
    font-weight: bold;
}

.user-profile__create-twoot{
  display: flex;
  flex-direction: column;
  padding-top: 20px;
}

h1{
    margin: 0;
}
</style>
