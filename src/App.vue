<script setup>
import { v4 as uuidv4 } from "uuid";
import { ref, reactive } from 'vue';
import TaskItem from '@/components/Task/Item.vue';

const task = ref("");
const tasks = reactive([]);
const addTask = () => {
    if (task.value !== "") {
        const item = {
            id: uuidv4(),
            title: task.value
        }
        tasks.unshift(item);
        task.value = "";
    }

};
const removeItem = (id) => {
    const index = tasks.findIndex((task) => {
        return task.id === id;
    });
    tasks.splice(index, 1);
};

</script>
<template>
    <main class="container mx-auto">
        <header class="m-2">
            <h1 class="text-6xl font-thin select-none">TODO!</h1>
            <div class="font-semibold select-none text-neutral-600">simple and studid todo app</div>
        </header>
        <form class="px-10 py-12 bg-white shadow-sm">
            <section class="flex">
                <input type="text" placeholder="做點重要的事吧..."
                    class="w-full text-2xl focus:outline-none input-lg input input-bordered" v-model="task" />
                <button class="text-xl btn-lg btn btn-neutral" @click.prevent="addTask">新增</button>
            </section>
        </form>

        <section class="px-10 py-6 mt-4 bg-white">
            <ul class="">
                <TaskItem v-on:remove-item="removeItem" v-for="(t, index) in tasks" :key="index" :task="t"></TaskItem>
            </ul>
        </section>
    </main>
</template>

<style scoped></style>
