<template>
  <div class="userprofile">
    <h1>@{{user.username}}</h1>
    <div class="userpfoile__adminbadge" v-if="user.isAdmin">Admin</div>
    <div class="userpfoile__extradetail">
      {{fullName}}
      <div class="userprofile__followercount">
        <strong>Followers:</strong>
        {{followers}}
      </div>
    </div>
    <button @click="followUser">Follow</button>
  </div>

  <div class="userprofile__twootswrapper">
    <h4>Twoots:</h4>
    <TwootItem
      v-for="twoot in user.twoots"
      :key="twoot.id"
      :username="user.username"
      :twoot="twoot"
      @favorite="toggleFavorite"
    />
  </div>
</template>

<script>
import TwootItem from "./TwootItem";

export default {
  name: "UserProfile",
  components: { TwootItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "Neo-Dragon",
        firstName: "Stephen",
        lastName: "McVicker",
        email: "mcvickerstephen@gmail.com",
        isAdmin: true,
        twoots: [
          { id: 1, content: "Twooter is amazing!" },
          { id: 2, content: "Anoter twoot here..." },
        ],
      },
    };
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavorite(id) {
      console.log("Favorited Twoot" + id);
    },
  },
  // Example of lifecycle method
  mounted() {
    console.log("UserProfile mounted...");
  },

  // Example of way to do something on data change
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower!`);
      }
    },
  },
};
</script>

<style>
.userprofile {
  width: 300px;
  padding: 2em;
  margin: 1em;
  background-color: #d6eedd;
  border-radius: 10px;

  display: flex;
  flex-direction: column;
  text-align: left;

  box-shadow: 0 6px 10px 0px #3d4f5241;
}

.userpfoile__adminbadge {
  background-color: #eb3b98;
  border-radius: 50vh;
  color: white;
  padding: 0.2em 1em;
  margin-right: auto;
  margin-bottom: 1em;
}

.userpfoile__extradetail {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.userprofile__twootswrapper {
  min-width: 50%;
}

@media only screen and (max-width: 768px) {
  .userprofile__twootswrapper {
    width: 100%;
  }
}

h1 {
  margin-top: 0px;
  color: #41b883;
}

button {
  padding: 0.8em 1em;
  margin-top: 1em;

  display: inline-flex;
  justify-content: center;
  align-items: center;

  border-radius: 16px;
  border: none;
  outline: none;

  text-transform: uppercase;
  font-weight: bold;
  background-color: #41b883;
  color: white;

  cursor: pointer;

  transition: all 0.2s;
}

button:active {
  transform: scale(0.96);
}
</style>