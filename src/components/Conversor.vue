<template>
    <div class="conversor">
        <div class="header">
            <div class="top">
                <div class="menu-button" @click="showAsideMenu = true">
                    <img src="../assets/menu.png" alt="menu button">
                </div>
                <div class="brand">
                    <img src="../assets/logo-conversor.png" alt="Logo Jooao Conversor">
                    <img src="../assets/title.png" alt="Conversor">
                </div>
            </div>
        </div>
        <div 
            :class="[
                'aside',
                { 
                    expand: showAsideMenu,
                    minimize: !showAsideMenu
                }
            ]"
        >
            <div class="title">
                <div class="aside-logo">
                    <img 
                        src="../assets/logo-conversor.png" 
                        alt="Logo Jooao Conversor" 
                        v-if="showAsideMenu"
                    >
                    <img 
                        src="../assets/title.png" 
                        alt="Conversor" 
                        v-if="showAsideMenu"
                    >
                </div>
                <div class="aside-close" @click="showAsideMenu = false">
                    <p>x</p>
                </div>
            </div>
            <h3>Sobre</h3>
            <p class="aboutText">
                Essa "pequena" aplicação foi criada com o intuito de colocar em prática o início dos meus estudos em VueJS. Para isso, "clonei" o layout do Google Tradutor, para que pudesse me inspirar, praticar (HTML e CSS) e ao mesmo tempo me divertir. Espero que esse projeto de alguma forma mostre principalmente a quem está iniciando os estudos em alguma tecnologia, que não é necessário pensar em grandes projetos para tirar algo do 'papel'.
            </p>
        </div>
        <div class="gray-square"></div>
        <div class="form">
            <div class="currency">

                <!-- CURRENCY ENTRY -->
                <div class="group1">
                    <ul class="menu">
                        <li 
                            v-for="currency in topCurrencys"
                            :key="(currency.id)"
                            @click="changeCurrency('currencyA', currency)"
                        >
                            <label
                                :for="currency.id"
                                :class="[
                                    'currency-menu',
                                    {
                                        'is--checked': currency === currencyA
                                    }
                                ]"
                            > 
                                {{ currency.currencySymbol }} {{ currency.id }}
                            </label>
                            <input
                                type="radio"                                
                                :id="currency.id"                         
                                hidden
                            >
                        </li>
                    </ul>
                    <span @click="modal1 = !modal1">
                        <div :class="{rotate: modal1}">
                            <img src="../assets/arrow-up.png">  
                        </div>
                    </span>
                </div>

                <!-- BUTTON SWITCH CURRENCY -->
                <div class="swap-button" @click="switchCurrency()">
                    <div class="swap"></div>
                </div>

                <!-- CURRENCY EXIT -->
                <div class="group2">
                    <ul class="menu">
                        <li 
                            v-for="currency in topCurrencys"
                            :key="(currency.id)"
                            @click="changeCurrency('currencyB', currency)"
                        >
                            <label 
                                :for="currency.id"
                                :class="[
                                    'currency-menu',
                                    {
                                        'is--checked': currency === currencyB
                                    }
                                ]"                                
                            >
                                {{ currency.currencySymbol }} {{ currency.id }}
                            </label>
                            <input
                                type="radio"
                                :id="currency.id"                            
                                hidden
                            >
                        </li>
                    </ul>
                    <span @click="modal2 = !modal2">
                        <div :class="{rotate: modal2}">
                            <img src="../assets/arrow-up.png">
                        </div>
                    </span>
                </div>
            </div>

            <!-- MODAL 1 -->

            <div class="all-currency" :class="{ moreCurrencys: modal1 }">
               <h3>Em breve mais moedas...</h3>
            </div>

            <!-- MODAL 2 -->
            <div class="all-currency" :class="{ moreCurrencys: modal2 }">
               <h3>Em breve mais moedas...</h3>
            </div>

            <!-- DISPLAY -->
            <div class="display">
                <div class="input-value">
                    <input type="number" v-model="coinA">
                    <p> {{ coinA.length }}/5000</p>
                </div>
                <div class="output-value">
                    <p> {{ coinB }} </p>
                </div>
            </div>

        </div>

        <!-- FEEDBACK -->

        <div class="feedback">
            <button @click="showModal=true">Enviar feedback</button>
            <modal 
                v-if="showModal"
                v-model="showModal" 
            >
                <div class="moddalTitle" slot="titlebar">
                    <h3>Enviar feedback</h3>
                </div>
                <div class="modalContent" slot="content">
                    <div class="modalDescription">
                        <span>O quê você está achando dessa aplicação?</span>
                        <span>Por favor, conte-me!</span>
                    </div>
                    <form 
                        :action="`mailto:joaostael@gmail.com?subject=Feedback%20Jooao%20Conversor&body=${feedbackText}`" 
                        method="post"
                    >                       
                        <textarea 
                            cols="30"
                            rows="10"
                            placeholder="Digite seu feedback..."
                            required
                            v-model="feedbackText"
                        />
                        <div class="buttons">
                            <button type="submit">Enviar</button>
                            <button  class="btn-cancel" @click.prevent="showModal = false" >Cancelar</button>
                        </div>                    
                    </form>
                </div>
            </modal>
        </div>

        <!-- MODAL FEEDBACK -->

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
                <p>Contribuir</p>
            </div>
        </footer>
    </div>
</template>

<script>
import Modal from '@kouts/vue-modal';
import '@kouts/vue-modal/dist/vue-modal.css';

export default {
    name: "Conversor",
    components: {
        Modal
    },
    data(){
        return {
            feedbackText: "",

            // coins
            coinA: "",
            coinB: "",

            // currency
            currencyA: {},
            currencyB: {},
            currencys: [],
            topCurrencys: [],

            // modais
            modal1: true,
            modal2: true,
            rotate: true,

            showModal: false,
            showAsideMenu: false
        };
    },
    async mounted () {
        await this.getCurrencys()
        
        this.arrangeTopCurrencys(this.currencys)

        this.currencyA = this.currencys?.BRL
        this.currencyB = this.currencys?.USD
    },
    computed: {
        from_to () {
            return `${this.currencyA?.id}_${this.currencyB?.id}`
        },
    },
    watch: {
        coinA (value) {
            const priceURL = `https://free.currconv.com/api/v7/convert?q=${this.from_to}&compact=ultra&apiKey=${process.env.VUE_APP_CURRCONV_TOKEN}`
            fetch(priceURL)
                .then(res => res.json())
                .then(json => {
                    let cotacao = json[this.from_to]
                    let price = (cotacao * parseFloat(value))
                    this.coinB = price ? this.priceFormatter(price) : ''
                })
        },
    },
    methods: {
        arrangeTopCurrencys(value) {
            const topCurrencys = [
                'BRL',
                'USD',
                'CAD',
                'EUR',
                'AUD',
                'CNY'                
            ]            
            if(Object.keys(value).length) {
                let arrayValue = Object.values(value)
                this.topCurrencys = arrayValue.filter(currency => {
                    if (topCurrencys.some(item => item === currency.id)) {
                        return currency
                    }
                }) 
            }
        },
        async getCurrencys() {
            const currencysURL = `https://free.currconv.com/api/v7/currencies?apiKey=${process.env.VUE_APP_CURRCONV_TOKEN}`
            this.currencys = await fetch(currencysURL)
                .then(res => res.json())
                .then(json => json.results)
        },
        priceFormatter (price) {
            return String(price.toFixed(2)).replace('.',',')
        },        
        changeCurrency(currency, value){
            this[currency] = value
        },
        switchCurrency() {
            let curA = this.currencyA 
            let curB = this.currencyB
            this.currencyA = curB
            this.currencyB = curA
        }
    }
};
</script>

<style src="./conversor.scss" lang="scss" scoped></style>
