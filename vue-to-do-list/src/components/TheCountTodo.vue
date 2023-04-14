<!-- eslint-disable vue/no-mutating-props -->
<script>
export default {
    name: "TodoCount",
    props: [
        "countTodo"
    ],
}
</script>
<template>
    <div class="container">
        <p>{{ countTodo }} task</p>
    </div>
</template>
<style scoped>
</style>