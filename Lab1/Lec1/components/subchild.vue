<template>
    <div>
        <h1>subchild App Component</h1>
        <h2>hello {{username}}</h2>
    </div>
</template>

<script>
export default {
    name: "subchildApp",
    inject: ['username'],
}
</script>

<style scoped>
</style>