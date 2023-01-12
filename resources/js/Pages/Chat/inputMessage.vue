<template>
    <div class="relative  m-1">
        <div class="w-full flex justify-between border-gray-50 border-t p-2">
            <input type="text" v-model="message" @keyup.enter="sendMessage()" placeholder="What's on your mind!"
                class="mx-2 w-full border-none focus:ring-0 outline-none p-1" />
            <button @click="sendMessage()"
                class="w-52 mx-2 bg-gray-500 hover:bg-teal-500 p-2 px-4 mt-1 rounded text-white"
                :disabled="btnDisabled">
                Send
                Message
            </button>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    props: {
        room: {
            type: Object,
            required: true
        }
    },
    data() {
        return {
            message: '',
            btnDisabled: false
        }
    },
    methods: {
        sendMessage() {
            if (!this.message) return;
            this.btnDisabled = true;
            const message = this.message;
            this.message = '';
            axios.post(`/chat/room/${this.room.id}/message`, {
                message
            })
                .then((res) => {
                    if (res.status == 201) {
                        this.$emit('messageSent');
                    }
                })
                .catch(err => console.log('send Message', err))
                .finally(() => this.btnDisabled = false);
        }
    }
}
</script>
