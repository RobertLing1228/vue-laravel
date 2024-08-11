<template>
    <div class="w-[200px] p-2 border rounded-lg shadow-lg">
        <span>id: {{ mock.id }}<br /></span> 
        <span>title: {{ mock.title }}</span>
        <hr />
        <span class=" text-sm font-mono">
            info:
            <span>by userID: {{ mock.userId }}</span>
            <span>was completed: {{ mock.completed ? "Yes" : "No" }}</span>
        </span>
    </div>
</template>

<script setup>
import { ref } from 'vue';


class mockObj {
    constructor() {
        this.userId = "";
        this.id = 0;
        this.title = "";
        this.completed = false;
    }
}
const props = defineProps({
    obj: {
        type: Object,
        required: true,
        default: () => new MockObj()
    }
});

let mock = ref(new mockObj());
mock.value = props.obj; 
</script>

<style lang="scss" scoped></style>