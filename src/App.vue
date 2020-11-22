<template>
    <div id="app">
        <nav>
            <div class="navigation__logo">
                Twooter
            </div>
            <div class="navigation__user">
                {{ user.username }}
            </div>
        </nav>
        <UserProfile />
    </div>
</template>

<script>
    import UserProfile from "./components/UserProfile";

    export default {
        name: 'App',
        components: { UserProfile },
        data() {
            return {
                user: {
                    username: '_rejuancse'
                }
            }
        }
    }
</script>

<style lang="scss">
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        display: flex;
        flex-direction: column;
        padding: 0 5%;

        nav {
            background: #e35c93;
            color: #fff;
            padding: 14px 20px;
            font-size: 20px;

            .navigation__logo {
                text-align: left;
                width: 50%;
                float: left;
                font-weight: bold;
            }

            .navigation__user {
                text-align: right;
                width: 50%;
                float: right;
            }
        }
    } 
</style>
