<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
      <h1 class="user-profile_username">@{{ user.username }}</h1>
      <div class="user-profile_admin-badge" v-if="user.isAdmin">admin</div>
      <div class="user-profile_admin-badge" v-else>user</div>
      <div class="user-profile_follower-count">
        <strong>Followers: </strong>{{ followers }}
      </div>
    </div>
    <div class="user-profile_twoots-wrapper">
        <TwootItem v-for="twoot in user.twoots" :key="twoot.id" :username="user.username" :twoot="twoot" />
      </div>
  </div>
</template>

<script>
import TwootItem from "./TwootItem"
export default {
  name: "UserProfile",
  components: { TwootItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "KoolBoiNathan",
        firstName: "Nathan",
        lastName: "Neil",
        email: "nathanneil66@gmail.com",
        isAdmin: true,
        twoots: [
          { id: 1, content: "Twotter is Amazing!" },
          { id: 2, content: "I'm Supa hot fire! " },
        ],
      },
    };
  },
  mounted() {
    this.followers++;
  },
  watch: {
    followers(oldFollowerCount, newFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower`);
      }
    },
  },
};
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}

.user-profile_user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dee3e8;
}

h1 {
  margin: 0;
}

.user-profile_admin-badge {
  background-color: rebeccapurple;
  color: white;
  border-radius: 10px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}
</style>
