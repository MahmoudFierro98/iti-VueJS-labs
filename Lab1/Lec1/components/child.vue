<template>
    <div>
        <h1>Child App Component</h1>
        <h2>{{name}}</h2>
        <h3>{{fname}}</h3>
        <h3>{{lname}}</h3>
        <h1>from child app {{username}}</h1>
        <subchildApp />
    </div>
</template>

<script>
import subchildApp from './subchild.vue'
export default {
    name: "childApp",
    props: ['name', 'fname', 'lname'],
    inject: ['username'],
    components: {
        subchildApp
    }
}
</script>

<style scoped>
</style>