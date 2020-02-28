<template>
    <div class="hello">
        <input type="text" v-model="backend" />
        <p v-if="random">random = {{ random }}</p>
        <p v-else>random = null</p>
        <p v-if="secret">secret = {{ secret }}</p>
        <p v-else>secret = null</p>
        <p v-if="hostname">hostname = {{ hostname }}</p>
        <p v-else>hostname = null</p>
        <button @click="loadRandom">Load random from API</button>
        <div class="error" v-if="error">
            {{ error }}
        </div>
    </div>
</template>

<script>
export default {
    name: 'HelloWorld',
    data() {
        return {
            backend: 'http://localhost:8081',
            random: '',
            secret: '',
            hostname: '',
            error: ''
        }
    },
    methods: {
        loadRandom() {
            fetch(`${this.backend}/random`)
                .then(res => res.json())
                .then(json => {
                    this.error = ''
                    this.random = json.random
                    this.secret = json.secret
                    this.hostname = json.hostname
                })
                .catch(err => {
                    this.error = err.message
                    this.random = ''
                    this.secret = ''
                    this.hostname = ''
                })
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
* {
    box-sizing: border-box;
}
p {
    font-family: monospace;
}

input {
    font-size: 1.3rem;
    padding: 0.2rem;
    width: 100%;
}

.error {
    color: tomato;
}
</style>
