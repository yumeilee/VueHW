<script setup>
import { ref } from 'vue';
import trashconIcan from '@/components/Icon/trashcanIcon.vue';

const props = defineProps({
    task: {
        type: Object,
        required: true,
    },
})

const emits = defineEmits(["remove-item"])
const remove = () => {
    emits('remove-item', props.task.id)

}
const isChecked = ref(false);

</script>

<template>
    <li class="flex items-center justify-between py-6 border-b">
        <div class="flex items-center gap-3">
            <input type="checkbox" id="todo_id_1" class="checkbox" v-model="isChecked" />
            <label class="text-xl cursor-pointer" :class="{ 'line-through': isChecked }">{{ task.title }}
            </label>
        </div>
        <div>
            <button class="p-2 hover:text-white hover:bg-neutral" @click="remove">
                <trashconIcan></trashconIcan>
            </button>
        </div>
    </li>
</template>
<style scoped>
.line-through {
    text-decoration: line-through;
}
</style>

