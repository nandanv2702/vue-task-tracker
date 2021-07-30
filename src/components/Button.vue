<template>
    <button class="btn" :style="{ 'background': color }">
        {{ text }}
    </button>
</template>

<script>
export default {
    name: 'Button',
    props: {
        text: String,
        color: String
    },
    methods: {
        onClick() {
            console.log('click')
        }
    }
}
</script>

<style scoped>

Button {
    width: 120px;
}

</style>