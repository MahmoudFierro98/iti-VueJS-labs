<template>
    <div>
        <h1>popup App Component</h1>
    </div>
    <div>
        <input type="text" v-model="name">
        <button @click="$emit('close', name)">close</button>
    </div>
</template>

<script>
    export default {
        name: "popupApp",
        emits: ['close'],
        data() {
            return {
                name: '',
            }
        },
    }
</script>

<style scoped>

</style>