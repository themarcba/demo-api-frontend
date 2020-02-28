<template>
    <div class="hello">
        <p v-if="random">random = {{ random }}</p>
        <p v-else>random = null</p>
        <p v-if="secret">secret = {{ secret }}</p>
        <p v-else>secret = null</p>
        <button @click="loadRandom">Load random from API</button>
    </div>
</template>

<script>
export default {
    name: 'HelloWorld',
    data() {
        return {
            random: '',
            secret: ''
        }
    },
    methods: {
        loadRandom() {
            fetch(`http://localhost:8081/random`)
                .then(res => res.json())
                .then(json => {
                    this.random = json.random
                    this.secret = json.secret
                })
                .catch(err => {
                    console.error(err.message)
                })
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
p {
    font-family: monospace;
}
</style>
