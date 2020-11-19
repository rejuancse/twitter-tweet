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
    .create-twoot-panel {
        margin-top: 20px;
        padding: 20px 0;
        display: flex;
        flex-direction: column;

        textarea {
            border: 1px solid #dfe3e8;
            border-radius: 5px;
        }

        .create-twoot-panel__submit {
            background: #e3e3e3;
        }

    }
    
</style>
