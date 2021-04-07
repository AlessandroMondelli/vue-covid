<template>
    <form>
        <label>Inserisci un paese</label>
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
        font-size: 22px;
        font-weight: bold;
        }

        #country {
            display: block;
            margin: 15px 0 0;
            border: 2px solid white;
            border-radius: 5px;
            padding: 10px 20px;
            background-color: rgba(255, 255, 255, 0.397);
            transition: 0.2s;

            &:hover {
                border-color: black;
            }
        }
    }
    
</style>