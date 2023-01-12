<script setup>
import ApplicationMark from './ApplicationMark.vue';
</script>

<template>
    <div>
        <div class="p-6 sm:px-20 bg-white border-b border-gray-200">

            <div class="mt-8 text-2xl flex items-center gap-x-4">
                <ApplicationMark class="block h-12 w-auto" />
                Welcome to Simple Chat App!
            </div>

            <div class="mt-6 text-gray-500 text-lg">
                Go to chat and start chatting in one of the chat rooms. You can select one from dropdown at the top.
            </div>
        </div>

    </div>
</template>
