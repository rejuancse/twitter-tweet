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
            <form class="user-profile__create-wrapper" @submit.prevent="createNewTwoot">
                <label for="newTwoot"><strong>New Twoot</strong></label>
                <textarea id="newTwoot" rows="4" v-model="newTwootContent" />

                <div class="user-profile__create-twoot-type">
                    <label for="newTwootType"><strong>Type: </strong></label>
                    <select id="newTwootType" v-model="selectTwootType">
                        <option :value="option.value" v-for="(option, index) in twootTypes" :key="index">
                            {{ option.name }}
                        </option>
                    </select>
                </div>
                <button>Twoot!</button>
            </form>

        </div>

        
        <div class="user-profile__twoots-wrapper">
            <TwootItem 
                v-for="twoot in user.twoots" 
                :key="twoot.id" 
                :username="user.username" 
                :twoot="twoot" 
                @favourite="toggleFavourite" 
            />
        </div>
    </div>
</template>

<script>
    import TwootItem from "./TwootItem";

    export default {
        name: 'UserProfile',
        components: { TwootItem },
        data() {
            return {
                newTwootContent: '',
                selectTwootType: 'instant',
                twootTypes: [
                    { value: 'draft', name: 'Draft' },
                    { value: 'instant', name: 'Instant Twoot' },
                ],
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
                        { id: 2, content: 'Twotter is Awesome!2' },
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
            },
            toggleFavourite(id) {
                console.log('Favourite', id)
            },
            createNewTwoot() {
                if(this.newTwootContent && this.selectTwootType !== 'draft') {

                    this.user.twoots.unshift({
                        id: this.user.twoots.length + 1,
                        content: this.newTwootContent,
                    })

                }
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
        padding: 50px 0;
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
    .user-profile__twoots-wrapper {
        display: grid;
        grid-gap: 10px;
    }
    .user-profile__create-wrapper {
        display: flex;
        flex-direction: column;
    }
</style>
