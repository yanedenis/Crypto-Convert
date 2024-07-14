<script>
export default {
    props: {
        favs: {
            type: Array,
            required: true,
        },
        getFavorites: {
            type: Function,
            required: true,
        }
    }
}
</script>
<template>
    <h2>Favorite</h2>
    <div className="pairs">
        <div v-for="(el, index) in favs" :key="index" className="pair" @click="getFavorites(index)">
            <span>{{ el.from }}</span>
            <svg fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.2"
                viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                <path d="m12.75 3 9 9-9 9v-4.5h-1.875v-9h1.875V3Z"></path>
                <path d="M4.125 16.5v-9"></path>
                <path d="M7.5 16.5v-9"></path>
            </svg>
            <span>{{ el.to }}</span>
        </div>
    </div>
</template>
<style scoped>
h2 {
    font-size: 52px;
    margin-top: 20px;
    margin-bottom: 12px;
}

.pairs {
    display: flex;
    flex-direction: column;
    gap: 8px;
    cursor: pointer;
}

.pair {
    margin: 0 auto;
    width: fit-content;
    background-color: var(--secondary);
    padding: 4px 18px;
    border-radius: 8px;
    display: flex;
    align-items: center;
    gap: 10px;
}

span {
    font-size: 38px;
    color: white;
}

svg {
    width: 30px;
    stroke: white;
}
</style>