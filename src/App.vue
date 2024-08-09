<script>
import Input from './components/Input.vue'
import Selector from './components/Selector.vue'
import Favorites from './components/Favorites.vue'
import CryptoConvert from 'crypto-convert';

const convert = new CryptoConvert();

export default {
    components: { Input, Selector, Favorites },
    data() {
        return {
            amount: null,
            crypto1: '',
            crypto2: '',
            error: '',
            result: null,
            favs: [],
        }
    },
    methods: {
        favorite() {
            if (this.crypto1 == this.crypto2) {
                this.error = 'Choose different currency';
                return;
            };
            
            for (let i = 0; i < this.favs.length; i++) {
                if (this.crypto1 === this.favs[i].from &&
                    this.crypto2 === this.favs[i].to) {
                        this.error = 'Already in favorites';
                        return;
                }
            }

            this.error = '';
            this.favs.push({
                from: this.crypto1,
                to: this.crypto2
            });
        },
        getFavorites(index) {
            this.crypto1 = this.favs[index].from
            this.crypto2 = this.favs[index].to
        },
        changeAmount(value) {
            this.amount = value
        },
        setCrypto1(value) {
            this.crypto1 = value
        },
        setCrypto2(value) {
            this.crypto2 = value
        },
        async convert() {
            if (this.amount <= 0) {
                this.error = 'Need number more than 0';
                this.result = '';
                return;
            } else if (this.crypto1 == '' || this.crypto2 == '') {
                this.error = 'Choose currency';
                this.result = '';
                return;
            } else if (this.crypto1 == this.crypto2) {
                this.error = 'Choose different currency';
                this.result = '';
                return;
            }
            this.error = '';

            await convert.ready();

            if (this.crypto1 == 'BTC' && this.crypto2 == 'ETH') {
                this.result = convert.BTC.ETH(this.amount);
            } else if (this.crypto1 == 'BTC' && this.crypto2 == 'USDT') {
                this.result = convert.BTC.USDT(this.amount);
            } else if (this.crypto1 == 'ETH' && this.crypto2 == 'BTC') {
                this.result = convert.ETH.BTC(this.amount);
            } else if (this.crypto1 == 'ETH' && this.crypto2 == 'USDT') {
                this.result = convert.ETH.USDT(this.amount);
            } else if (this.crypto1 == 'USDT' && this.crypto2 == 'BTC') {
                this.result = convert.USDT.BTC(this.amount);
            } else if (this.crypto1 == 'USDT' && this.crypto2 == 'ETH') {
                this.result = convert.USDT.ETH(this.amount);
            }
        }
    }
};
</script>

<template>
    <main>
        <h1>CRYPTO</h1>
        <p v-show="error != ''">{{ error }}</p>
        <p v-show="result != 0">{{ result }}</p>
        <Input :changeAmount="changeAmount" />
        <div className="selectors">
            <Selector :setCrypto="setCrypto1" :cryptoNow="crypto1"/>
            <div class="options">
                <button @click="convert()">
                    <svg fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"
                        stroke-width="1.2" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                        <path d="M7.5 15h12a.75.75 0 0 0 .75-.75V4.5a.75.75 0 0 0-.75-.75H9a.75.75 0 0 0-.75.75v.75">
                        </path>
                        <path d="M9.75 12.75 7.5 15l2.25 2.25"></path>
                        <path d="M16.5 9h-12a.75.75 0 0 0-.75.75v9.75a.75.75 0 0 0 .75.75H15a.75.75 0 0 0 .75-.75v-.75">
                        </path>
                        <path d="M14.25 11.25 16.5 9l-2.25-2.25"></path>
                    </svg>
                </button>
                <button @click="favorite()">
                    <svg fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"
                        stroke-width="1.2" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                        <path
                            d="M12 20.25S2.625 15 2.625 8.625A4.875 4.875 0 0 1 12 6.75v0a4.875 4.875 0 0 1 9.375 1.875C21.375 15 12 20.25 12 20.25Z">
                        </path>
                    </svg>
                </button>
            </div>
            <Selector :setCrypto="setCrypto2" :cryptoNow="crypto2"/>
        </div>
        <Favorites :favs="favs" v-if="favs.length > 0" :getFavorites="getFavorites"/>
    </main>
</template>

<style scoped>
h1 {
    font-size: 7em;
}

.selectors {
    display: flex;
    gap: 40px;
    justify-content: center;
    height: min-content;
    align-items: center;
}

.options {
    display: grid;
    grid-column: auto;
}

.options button {
    height: fit-content;
    background-color: transparent;
    border: 0;
    cursor: pointer;
    outline: 0;
}

.options button:nth-child(2) svg:hover {
    fill: currentColor;
}

p {
    font-size: 20px;
}

svg {
    width: 56px;
}
</style>
