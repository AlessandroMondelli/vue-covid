<template>
    <form>
        <label>Verifica i dati del contagio COVID-19</label>
        <input type="text" name="country" id="country" placeholder="Inserisci un paese..." v-model.trim="countryInput" @keyup="sendCountry">
    </form>
</template>

<script>
export default {
    name: "SearchCountry",
    data() {
        return {
            countryInput: '',
        }
    },
    methods: {
        sendCountry() {
            this.$emit('country-value', this.countryInput); //Invio al padre paese scelto
        }
    }
}
</script>

<style lang="scss" scoped>
    form {
        padding: 20px 0 0;
        margin-bottom: 50px;

        label {
            font-weight: bold;
        }

        input {
            width: 60%;
            margin-top: 10px;
            text-align: center;
        }

        #country {
            display: block;
            border: 2px solid white;
            border-radius: 5px;
            padding: 10px 20px;
            background-color: #AB3938;
            transition: 0.2s;

            &:hover {
                border-color: black;
            }
        }
    }

    $breakpoint-smartphone: 320px;
    $breakpoint-tablet: 767px;
    $breakpoint-laptop: 992px;
    $breakpoint-large: 1200px;

    @media (min-width: $breakpoint-smartphone) {
        label {
            font-size: 16px;
        }

        input {
            margin-left: 50%;
            transform: translate(-50%);
            height: 10px;
        }
    }

    @media (min-width: $breakpoint-tablet) {
        label {
            font-size: 20px;
        }

        input {
            height: 30px;
        }
    }

     @media (min-width: $breakpoint-laptop) {
        label {
            font-size: 28px;
        }

        input {
            height: 30px;
        }
    }
    
</style>