<template>
    <div>
        <h1>Reactive expample: {{ count }}</h1>
        <div>
            <button @click="increment">Increment</button>
        </div>
        <ul>
            <li v-for="item in list">{{ item }}</li>
        </ul>
    </div>
</template>

<script setup>
import { reactive, toRefs } from 'vue';

let obj = reactive({ count: 1, list: ['Learn'] });
//dont destructure without toRefs
let { count, list } = toRefs(obj);

function increment() {
    console.log("hello")
    count.value++;
}
</script>
