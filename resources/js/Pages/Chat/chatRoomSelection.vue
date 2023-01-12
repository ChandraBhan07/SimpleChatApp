<script setup>

</script>

<template>
    <div class="flex items-center justify-between">
        <div class="font-bold text-xl">
            {{ selected.name }} Chat
        </div>
        <div>
            <select v-model="selected" @change="$emit('roomChanged', selected)"
                class="border-none focus:ring-0 outline-none">
                <option v-for="(room, index) in rooms" :key="index" :value="room">
                    {{ room.name }}
                </option>
            </select>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        rooms: {
            type: Array,
            required: true
        },
        currentRoom: {
            type: Object,
            required: true
        }
    },
    data() {
        return {
            selected: ''
        }
    },
    created() {
        this.selected = this.currentRoom;
    }
}
</script>