<template>
    <div class="conversor">
        <div class="header">
            <div class="top">
                <div class="menu-button">
                    <img src="../assets/menu.png" alt="menu button">
                </div>
                <div class="brand">
                    <img src="../assets/logo-conversor.png" alt="Logo Jooao Conversor">
                    <img src="../assets/title.png" alt="Conversor">
                </div>
            </div>
        </div>
        <div class="gray-square"></div>
        <div class="form">
            <div class="currency">
                <div class="group1">
                    <ul class="menu">

                        <li v-for="currency in currencys" :key="currency.id"> <a href="#">  {{ currency.label }} </a> </li> 

                    </ul>
                    <span><img src="../assets/arrow-down.png" alt="seta para clique"></span>
                      
                </div>
                <div class="swap-button">
                    <div class="swap">

                    </div>
                </div>
                <div class="group2">
                    <ul class="menu">

                        <li v-for="currency in currencys" :key="currency.label"> <a href="#"> {{ currency.label }} </a> </li>
                       
                    </ul>
                    <span><img src="../assets/arrow-down.png" alt="seta para clique"></span>
                </div>
            </div>
            <div class="display">
                <div class="input-value">
                    <input type="number" v-model="coinA">
                    <p> {{ coinA.length }} /5000</p>
                </div>
                <div class="output-value">
                    <p> {{ coinB }} </p>
                </div>
            </div>
            
        </div>
        <div class="feedback">
            <a href="#"><em>Enviar feedback</em></a>
        </div>
        <footer>
            <div>
                <div class="circle">
                    <a href="#"><img src="../assets/past.png" alt="histórico"></a>
                </div>
                <p>Histórico</p>
            </div>
            <div>
                <div class="circle">
                    <a href="#"><img src="../assets/star.png" alt=""></a>
                </div>
                <p>Salvas</p>
            </div>
            <div>
                <div class="circle">
                    <a href=""><img src="../assets/community.png" alt="comunidade"></a>
                </div>
                <p>Comunidade</p>
            </div>
        </footer>
    </div>
</template>

<script>
export default {
    name: "Conversor",
    props: {
        currencyA: {
            type: String,
            default: ''
        },
        currencyB: {
            type: String,
            default: ''
        }
    },
    data(){
        return {
            coinA: "",
            coinB: "",
            from_to: '',
            url: '',
            currencys: [
                { id: 1, label: 'USD' },
                { id: 2, label: 'BRL' },
                { id: 3, label: 'CAD' },
                { id: 4, label: 'EUR' },
                { id: 5, label: 'GBP' },
                { id: 6, label: 'JPY' },
                { id: 7, label: 'AUD' },
                { id: 8, label: 'CHF' },
                { id: 9, label: 'CNH' },
                { id: 10, label: 'ARS' },
                { id: 11, label: 'TRY' },
                { id: 12, label: 'NZD' },
                { id: 13, label: 'RUB' },
                { id: 14, label: 'ZAR' },
                { id: 15, label: 'MXN' },
                { id: 16, label: 'CLP' },
                { id: 17, label: 'COP' },
                { id: 18, label: 'PEN' },
                { id: 19, label: 'PYG' },
                { id: 20, label: 'SEK' },
                { id: 21, label: 'UYU' },
                { id: 22, label: 'VEF' },
                { id: 23, label: 'XAF' },
                { id: 24, label: 'XCD' },
            ]
        };
    },
    mounted () {
        this.from_to = `${this.currencyA}_${this.currencyB}`
        this.url = "https://free.currconv.com/api/v7/convert?q=" + this.from_to + "&compact=ultra&apiKey=ff13ef5114b17bd0ea42"
    },
    watch: {
        coinA (value) {
            fetch(this.url)
                .then(res => res.json())
                .then(json => {
                    let cotacao = json[this.from_to]
                    let price = (cotacao * parseFloat(value))
                    this.coinB = price ? this.priceFormatter(price) : ''
                })
        }
    },
    methods: {
        priceFormatter (price) {
            return String(price.toFixed(2)).replace('.',',')
        }
    }
};
</script>

<style src="./conversor.scss" lang="scss" scoped></style>
