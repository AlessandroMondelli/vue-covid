<template>
    <section id="italian-data">
        <h2>Italy</h2>
        <div class="covid-data">
            <p class="inner-data"><strong>Casi Totali:</strong> {{ covidCasesLive }}</p>
            <p class="inner-data"><strong>Infetti Attivi:</strong> {{ covidActiveLive }}</p>
            <p class="inner-data"><strong>Morti:</strong> {{ covidRecoveredLive }}</p>
            <p class="inner-data"><strong>Guariti:</strong> {{ covidDeathsLive }}</p>
        </div>
    </section>
</template>

<script>
import axios from 'axios';

export default {
    name: "ItalianData",
    data() {
        return {
            covidCasesLive: 0,
            covidActiveLive: 0,
            covidRecoveredLive: 0,
            covidDeathsLive: 0,
        }
    },
    mounted() {
        var MyDate = new Date();

        var yesterday = (MyDate.getFullYear() + '-' + ('0' + (MyDate.getMonth()+1)).slice(-2) + '-' + ('0' + (MyDate.getDate() - 1)).slice(-2)) + 'T00:00:00Z';
        var twoDaysAgo = (MyDate.getFullYear() + '-' + ('0' + (MyDate.getMonth()+1)).slice(-2) + '-' + ('0' + (MyDate.getDate() - 2)).slice(-2)) + 'T00:00:00Z';

        const options = { //Parametri API
            method: 'GET',
            url: 'https://api.covid19api.com/live/country/italy/status/confirmed',
            params: {from: twoDaysAgo, to: yesterday},
            headers: {
                'X-Access-Token': '5cf9dfd5-3449-485e-b5ae-70a60e997864',
            }
        };

        axios.request(options).then( (response) => { //Chiamata Axios con parametri citati in precedenza
            console.log("in Axios:" + yesterday);
            console.log(response.data);
            
            var totalCases = 0;
            var totalActive = 0;
            var totalDeaths = 0;
            var totalRecovered = 0;

            response.data.forEach(element => { //Se la chiamata ha avuto successo, foreach per data
                if(element.Date == yesterday) { //Se è la data di ieri
                    totalCases += element.Confirmed; //Salvo in variabile dati Casi
                    totalActive += element.Active; //Salvo in variabile dati Infetti attivi
                    totalDeaths += element.Deaths; //Salvo in variabile dati morti
                    totalRecovered += element.Recovered; //Salvo in variabile dati Guariti
                }
            });

            //Passo a variabile in Data() con numeri separati da punto
            this.covidCasesLive = totalCases.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.'); 
            this.covidActiveLive = totalActive.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.'); 
            this.covidRecoveredLive = totalDeaths.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.'); 
            this.covidDeathsLive = totalRecovered.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.'); 

        }).catch(function (error) { //Se si è verificato un errore
            console.error(error);
        });
    }
}
</script>

<style lang="scss">
    #italian-data {
        border: 2.5px solid white;
        border-radius: 3px;
        padding: 20px;

        .inner-data {
            font-size: 20px;
            margin: 10px 0 0;
        }
    }
</style>