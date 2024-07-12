<script>
export default {
    props: {
        changeAmount: {
            type: Function,
            required: true,
        }
    }
}
</script>

<template>
    <input type="number" @input="changeAmount($event.target.value)" min="0">
</template>

<style scoped>
input {
    border: 0;
    outline: 0;
    border-radius: 6px;
    font-size: 18px;
    background-color: var(--text);
    color: var(--background);
    padding: 8px 10px;
    width: 460px;
}
</style>
