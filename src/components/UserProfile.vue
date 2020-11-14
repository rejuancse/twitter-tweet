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
        </div>

        <div class="user-profile__twoots-wrapper">
            <div class="user-profile__twoot" v-bind:key="twoot.id" v-for="twoot in user.twoots">
                {{ twoot.content }}
            </div>
        </div>
        
        <!-- <button @click="followUser">Follow</button> -->
    </div>
</template>

<script>
    export default {
        name: 'UserProfile',
        data() {
            return {
                followers: 0,
                user: {
                    id: 1,
                    username: '_rejuancse',
                    firstName: 'Rejuan',
                    lastName: 'Ahamed',
                    email: 'rejuancse@gmail.com', 
                    isAdmin: true,
                    twoots: [
                        { id: 1, content: 'Twotter is Amazing' },
                        { id: 2, content: 'Twotter is Awesome!' }
                    ]
                }
            }
        },

        watch: {
            followers(newFollowers, oldFollowers) {
                if(oldFollowers < newFollowers) {
                    console.log(`${this.user.username} has gained a Follower!`)
                }
            }
        },

        computed: {
            fullname() {
                return `${this.user.firstName} ${this.user.lastName}`;
            }
        },

        methods: {
            followUser() {
                this.followers++
            }
        },

        mounted() {
            this.followUser();
        }
    }
</script>

<style>
    .user-profile {
        display: grid;
        grid-template-columns: 1fr 3fr;
        width: 100%;
        padding: 50px 5%;
        text-align: left;
    }
    .user-profile__user-panel {
        display: flex;
        flex-direction: column;
        margin-right: 50px;
        padding: 20px;
        background-color: white;
        border-radius: 5px;
        border: 1px solid #dfe3e8;
    }
    .user-profile__admin-badge {
        background: red;
        color: #ffffff;
        border-radius: 5px;
        margin-right: auto;
        margin-top: 6px;
        margin-bottom: 6px;
        padding: 3px 10px;
        font-weight: bold;
    }
    h1 {
        margin: 0;
    }
</style>
