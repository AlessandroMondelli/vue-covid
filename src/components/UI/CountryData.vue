<template>
    <div class="country-data" v-if="countrySelectedPass.length != 0 || countryInput.length != 0">
        <div v-if="error == false && covidCasesLive != 0" id="success-data">
            <h2>{{ countrySelectedPass }}, dati aggiornati al {{ date }}</h2>
            <div class="covid-data">
                <p class="inner-data"><strong>Casi Totali</strong> <span class="single-data">{{ covidCasesLive }}</span> <span :class="[ covidNewCases > 0 ? positive : negative]">{{ covidNewCases }}</span></p>
                <p class="inner-data"><strong>Infetti Attivi</strong> <span class="single-data">{{ covidActiveLive }}</span> <span :class="[ covidNewActive > 0 ? positive : negative]">{{ covidNewActive }}</span></p>
                <p class="inner-data"><strong>Morti</strong> <span class="single-data">{{ covidDeathsLive }}</span> <span :class="[ covidNewDeaths > 0 ? positive : negative]">{{ covidNewDeaths }}</span></p>
                <p class="inner-data"><strong>Guariti</strong> <span class="single-data">{{ covidRecoveredLive }}</span> <span :class="[ covidNewRecovered >= 0 ? positive : negative]">{{ covidNewRecovered }}</span></p>
            </div>
        </div>
        <div v-else id="error-data">
            <p>Ops! Non abbiamo trovato il paese desiderato</p>
            <p v-if="errorLog.length != 0">Errore: {{ errorLog }}</p>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "CountryData",
    props:['countrySelectedPass'],
    data() {
        return {
            countryInput: '',
            covidCasesLive: 0,
            covidActiveLive: 0,
            covidRecoveredLive: 0,
            covidDeathsLive: 0,
            covidNewCases: 0,
            covidNewActive: 0,
            covidNewRecovered: 0,
            covidNewDeaths: 0,
            error: false,
            errorLog: '',
            date: '',
            positive: 'positive',
            negative: 'negative',
        }
    },
    methods: {
        getCovidData(country) {
            var MyDate = new Date();

            var yesterday = (MyDate.getFullYear() + '-' + ('0' + (MyDate.getMonth()+1)).slice(-2) + '-' + ('0' + (MyDate.getDate() - 1)).slice(-2)) + 'T00:00:00Z';
            this.date = (('0' + (MyDate.getDate() - 1)).slice(-2) + '-' + ('0' + (MyDate.getMonth()+1)).slice(-2) + '-' + MyDate.getFullYear());
            var twoDaysAgo = (MyDate.getFullYear() + '-' + ('0' + (MyDate.getMonth()+1)).slice(-2) + '-' + ('0' + (MyDate.getDate() - 2)).slice(-2)) + 'T00:00:00Z';

            const options = { //Parametri API
                method: 'GET',
                url: 'https://api.covid19api.com/live/country/' + country + '/status/confirmed',
                params: {from: twoDaysAgo, to: yesterday},
                headers: {
                    'X-Access-Token': '5cf9dfd5-3449-485e-b5ae-70a60e997864',
                }
            };

            axios.request(options).then((response) => { //Chiamata Axios con parametri citati in precedenza
                var totalCases = 0;
                var totalActive = 0;
                var totalDeaths = 0;
                var totalRecovered = 0;

                var totalCasesTwoDaysAgo = 0;
                var totalActiveTwoDaysAgo = 0;
                var totalDeathsTwoDaysAgo = 0;
                var totalRecoveredTwoDaysAgo = 0;

                response.data.forEach(element => { //Se la chiamata ha avuto successo, foreach per data
                    if(element.Date == yesterday) { //Se è la data di ieri
                        totalCases += element.Confirmed; //Salvo in variabile dati Casi
                        totalActive += element.Active; //Salvo in variabile dati Infetti attivi
                        totalDeaths += element.Deaths; //Salvo in variabile dati morti
                        totalRecovered += element.Recovered; //Salvo in variabile dati Guariti
                    } else if(element.Date == twoDaysAgo) { //Se la data è di due giorni fa
                        totalCasesTwoDaysAgo += element.Confirmed; //Salvo in variabile dati Casi
                        totalActiveTwoDaysAgo += element.Active; //Salvo in variabile dati Infetti attivi
                        totalDeathsTwoDaysAgo += element.Deaths; //Salvo in variabile dati morti
                        totalRecoveredTwoDaysAgo += element.Recovered; //Salvo in variabile dati Guariti
                    }
                });

                //Passo a variabile in Data() con numeri separati da punto
                this.covidCasesLive = totalCases.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.'); 
                this.covidActiveLive = totalActive.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.'); 
                this.covidRecoveredLive = totalRecovered.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.'); 
                this.covidDeathsLive = totalDeaths.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.'); 

                //Valore differenza tra i due giorni
                this.covidNewCases = totalCases - totalCasesTwoDaysAgo; 
                this.covidNewActive = totalActive - totalActiveTwoDaysAgo;
                this.covidNewRecovered = totalRecovered - totalRecoveredTwoDaysAgo; 
                this.covidNewDeaths = totalDeaths - totalDeathsTwoDaysAgo;

            }).catch((error) => { //Se si è verificato un errore
                this.error = true;
                this.errorLog = error;
            });
        }
    },
    watch: {
        countrySelectedPass: function(newVal) {
            this.countryInput = newVal; //Assegno a variabile paese inserito in "SearchCountry"
            this.getCovidData(this.countryInput); //Richiamo method all'arrivo di un nuovo paese
        }
    },
    mounted() {
        this.getCovidData(this.countrySelectedPass);
    }
}
</script>

<style lang="scss">
    .country-data {
        border: 2.5px solid white;
        border-radius: 5px;
        padding: 20px;
        


        .inner-data {
            font-size: 20px;
            margin: 10px 0 0;
            display: grid;
            grid-template-columns: 25% 25% 25%;
            column-gap: 15px;

            .positive {
              color: rgb(204, 48, 48);  
            }

            .negative {
                color: rgb(50, 172, 45);
            }
        }
            
    }
</style>