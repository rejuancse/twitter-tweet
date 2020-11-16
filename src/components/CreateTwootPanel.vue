<template>
    <form class="user-profile__create-wrapper" @submit.prevent="createNewTwoot" :class="{ '--exceeded': newTwootCharacterCount > 180 }">
        <label for="newTwoot"><strong>New Twoot</strong> ({{ newTwootCharacterCount }}/180) </label>
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
</template>

<script>
    export default {
        name: 'CreateTwootPanel',
        data() {
            return {
                newTwootContent: '',
                selectTwootType: 'instant',
                twootTypes: [
                    { value: 'draft', name: 'Draft' },
                    { value: 'instant', name: 'Instant Twoot' },
                ],
            }
        },

        computed: {
            newTwootCharacterCount() {
                return this.newTwootContent.length;
            }
        },

        methods: {
            createNewTwoot() {
                if(this.newTwootContent && this.selectTwootType !== 'draft') {
                    this.$emit('add-twoot', this.newTwootContent)
                    this.newTwootContent = '';
                }
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
                background: red;
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
