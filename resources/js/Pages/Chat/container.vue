<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import MessageContainer from './messageContainer.vue';
import InputMessage from './inputMessage.vue';
import ChatRoomSelection from './chatRoomSelection.vue';
import axios from 'axios';
import { onMounted } from 'vue';

</script>

<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                <chat-room-selection v-if="currentRoom.id" :rooms="chatRooms" :currentRoom="currentRoom"
                    v-on:roomChanged="setRoom($event)" />
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                    <message-container :messages="messages" />
                    <input-message :room="currentRoom" v-on:messageSent="getMessages()" />
                </div>
            </div>
        </div>
    </AppLayout>
</template>

<script>
export default {
    setup() {
        onMounted(() => console.log('text'));
    },

    data: function () {
        return {
            chatRooms: [],
            currentRoom: [],
            messages: []
        }
    },

    watch: {
        currentRoom(val, oldVal) {
            if (oldVal.id) {
                this.disconnect(oldVal);
            }
            this.connect();
        }
    },

    methods: {
        getRoooms() {
            axios.get('/chat/rooms')
                .then(res => {
                    this.chatRooms = res.data;
                    this.setRoom(res.data[0]);
                })
                .catch(err => {
                    console.log(err);
                });
        },

        getMessages() {
            axios.get(`/chat/room/${this.currentRoom.id}/messages`)
                .then(res => {
                    this.messages = res.data;
                })
                .catch(err => console.log('Messages', err));
        },

        setRoom(room) {
            this.currentRoom = room;
        },

        connect() {
            if (this.currentRoom.id) {
                this.getMessages();
                Echo.private(`chatroom-${this.currentRoom.id}`)
                    .listen('.NewMessage', e => {
                        console.log(e);
                        this.getMessages();
                    });
            }
        },

        disconnect(room) {
            console.log('disconnected ', room.id);
            Echo.leave(`chatroom-${room.id}`)
        }
    },

    created() {
        console.log('yes');
    },

    mounted() {
        console.log('test');
        this.getRoooms();
    }
}
</script>
