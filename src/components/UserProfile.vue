<template>
    <div class="user-profile">
        <div class="user-profile__sidebar">
            <div class="user-profile__user-panel">
                <h1 class="user-profile__username">@{{ user.username }}</h1>
                <div class="user-profile__admin-badge" v-if="user.isAdmin">
                    Admin
                </div> 
                <div class="user-profile__follower-count">
                    <strong>Followers: </strong> {{ followers }}
                </div>
            </div>
            <CreateTwootPanel @add-twoot="addTwoot" />
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
    import CreateTwootPanel from "./CreateTwootPanel";

    export default {
        name: 'UserProfile',
        components: { TwootItem, CreateTwootPanel },
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
                        { id: 2, content: 'Twotter is Awesome!2' },
                    ]
                }
            }
        }, 

        methods: {
            addTwoot(twoot) {
                this.user.twoots.unshift( {id: this.user.twoots.length + 1, content: twoot});
            }
        },
        
    }
</script>

<style lang="scss" scoped>
    .user-profile {
        display: grid;
        grid-template-columns: 1fr 3fr;
        width: 100%;
        padding: 50px 0;
        text-align: left;

        .user-profile__user-panel {
            display: flex;
            flex-direction: column;
            margin-right: 50px;
            padding: 20px;
            background-color: white;
            border-radius: 5px;
            border: 1px solid #dfe3e8;

            h1 {
                margin: 0;
            }

            .user-profile__admin-badge {
                background: rgb(135, 115, 245);
                color: #ffffff;
                border-radius: 5px;
                margin-right: auto;
                margin-top: 6px;
                margin-bottom: 6px;
                padding: 3px 10px;
                font-weight: bold;
            }

            .user-profile__create-wrapper {
                display: flex;
                flex-direction: column;

                &.--exceeded {
                    color: red;
                    border-color: red;

                    button {
                        background-color: red;
                        border: none;
                        color: white;
                    }
                }
            }
        }

        .user-profile__twoots-wrapper {
            display: grid;
            grid-gap: 10px;
        }
    }
    
</style>
