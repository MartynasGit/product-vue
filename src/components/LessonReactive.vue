<template>
    <div>
        <h1>Reactive expample: {{ count }}</h1>
        <div>
            <button @click="increment">Increment</button>
        </div>
    </div>
</template>

<script setup>
import { reactive, toRefs } from 'vue';

let obj = reactive({ count: 1, list: ['Learn'] });

let { count } = toRefs(obj);

function increment() {
    console.log("hello")
    count.value++;
}
</script>
