<template>
    <div class="user-profile">
        <div class="user-profile__sidebar">
            <div class="user-profile__user-panel">
                <h1 class="user-profile__username">@{{ this.user.username }}</h1>
                <div class="user-profile__admin-badge" v-if="this.user.isAdmin">
                    Admin
                </div>
                <div class="user-profile__follower-count">
                    <strong>Followers: </strong> {{ this.followers }}
                </div>
            </div>
            <!--<CreateTwootPanel @add-twoot="addTwoot" />-->
        </div>
        <div class="user-profile__twoots-wrapper">
            <TwootItem v-for="twoot in this.user.twoots" :key="twoot.id" :username="this.user.username" :twoot="twoot"
                @favourite="toggleFavourite" />
        </div>
    </div>
</template>

<script>
import TwootItem from './TwootItem.vue'
export default {
    name: 'UserProfile',
    components: {
        TwootItem
    },
    data() {
        return {
            followers: 0,
            user: {
                id: 1,
                username: 'RenatoCipriano',
                firstName: 'Renato',
                lastName: 'Cipriano',
                email: 'mail@mail.com',
                isAdmin: true,
                twoots: [
                    { id: 1, content: 'Twooter is Amazing!' },
                    { id: 2, content: "Don't forget to subscriber to The Earth is Square" },
                ]
            }
        }
    },
    watch: {
        followers(newFollowerCount, oldFollowerCount) {
            if (oldFollowerCount < newFollowerCount) {
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
        followUser() {
            this.followers++;
        },
        toggleFavourite(id) {
            console.log(`Favourited Tweet #${id}`);
        }
    },
    mounted() {
        this.followUser();
    }
}
</script>

<style scoped>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    grid-gap: 50px;
    padding: 50px 5%;
}

.user-profile .user-profile__user-panel {
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
    margin-bottom: auto;
}

.user-profile .user-profile__user-panel h1 {
    margin: 0;
}

.user-profile .user-profile__user-panel .user-profile__admin-badge {
    background: rebeccapurple;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
    font-weight: bold;
}

.user-profile .user-profile__twoots-wrapper {
    display: grid;
    grid-gap: 10px;
    margin-bottom: auto;
}
</style>
<!--
<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-gap: 50px;
  padding: 50px 5%;
  .user-profile__user-panel {
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
    margin-bottom: auto;
    h1 {
      margin: 0;
    }
    .user-profile__admin-badge {
      background: rebeccapurple;
      color: white;
      border-radius: 5px;
      margin-right: auto;
      padding: 0 10px;
      font-weight: bold;
    }
  }
  .user-profile__twoots-wrapper {
    display: grid;
    grid-gap: 10px;
    margin-bottom: auto;
  }
}
</style>
-->