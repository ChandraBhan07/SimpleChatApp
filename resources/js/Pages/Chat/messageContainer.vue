<script setup>
import messageItem from './messageItem.vue';
</script>

<template>
    <div class="h-96 w-full">
        <div class="h-full p-2 py-4 flex flex-col-reverse overflow-scroll overflow-x-hidden bg-neutral-200">
            <div v-for="(message, index) in messages" :key="index">
                <message-item :message="message" :authUser="authUser" />
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        messages: {
            type: Object,
            required: true
        }
    },

    data() {
        return {
            authUser: {}
        }
    },

    created() {
        axios.get('/auth/getUser')
            .then((res) => this.authUser = res.data)
            .catch(err => console.log('auth/getUser', err));
    }
}
</script>
