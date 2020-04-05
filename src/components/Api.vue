<template>
    <div id="app">
        <h1>Hola Internet</h1>
        
        <section v-if="errored">
            <p>No lo pude load! Try again later</p>
        </section>
        <section v-else>
            <div v-if="loading">Loading...</div>

            <div
                v-else
                v-for="info in info"
                :key="info.id"
                class="currency">
                {{ info.name }}:
                <span class="lighten">{{ info.age }}</span>
            </div>
        </section>    
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            info: null,
            loading: true,
            errored: false
        }
    },
    mounted() {
        axios
            .get('#')
            .then(response => (this.info = response.data.test))
            .catch(error => {
                console.log(error)
                this.errored = true
            })
            .finally(() => this.loading = false)
    }
}
</script>

<style>

</style>
