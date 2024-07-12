<script>
export default {
    props: {
        setCrypto: {
            type: Function,
            required: true,
        }
    },
    data() {
        return {
            currentValue: '',
        }
    },
    methods: {
        selectValue(value) {
            this.setCrypto(value);
            this.currentValue = value;
        }
    }
}
</script>

<template>
    <ul>
        <li @click="selectValue('BTC')" :className="currentValue == 'BTC' ? 'active' : ''">Bitcoin</li>
        <li @click="selectValue('ETH')" :className="currentValue == 'ETH' ? 'active' : ''">ETH</li>
        <li @click="selectValue('USDT')" :className="currentValue == 'USDT' ? 'active' : ''">USDT</li>
    </ul>
</template>

<style scoped>
ul {
    list-style: none;
    padding: 0;
    font-size: 22px;
    width: 180px;
    border: 3px var(--primary) solid;
}
li {
    display: block;
    padding: 12px 0;
    color: var(--primary);
}
li:nth-child(2) {
    border: 1px var(--primary) solid;
    border-left: 0;
    border-right: 0;
}
li:hover, li.active {
    background-color: var(--primary);
    color: var(--background);
    cursor: pointer;
}
</style>
