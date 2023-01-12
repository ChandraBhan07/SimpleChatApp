<script setup>
import axios from 'axios';


</script>

<template>
    <div class="p-2 px-4 flex" :class="message.user.name != authUser.name ? 'flex-row-reverse' : ''">
        <span class="bg-white rounded-b-2xl flex-inline items-center p-3 px-5"
            :class="message.user.name == authUser.name ? 'rounded-tr-2xl' : 'rounded-tl-2xl bg-teal-400 text-white'">
            {{ message.user.name }} :
            {{ message.message }}
            {{}}
        </span>

    </div>
</template>

<script>
export default {
    props: {
        message: {
            type: Object,
            required: true
        },
        authUser: {
            type: Object,
            required: true
        }
    },

}
</script>
