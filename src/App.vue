<template>
  <div id="app">
    <img class="logo" src="@/assets/lock.png" alt="Lock">
    <div class="form">
      <div class="form-item">
        <label>Seed</label>
        <input v-model="seed" />
      </div>
      <div class="form-item">
        <label>Cipher length</label>
        <input type="number" v-model="cipherLength" />
      </div>
      <div class="form-item result-box">
        <label>Generated key</label>
        <div class="result">
          {{ cipherKey }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      seed: '',
      cipherLength: 0,
    }
  },
  computed: {
    cipherKey() {
      return this.generateKey(this.cipherLength, this.stringToSeed(this.seed));
    }
  },
  methods: {
    generateKey(length, seed = 0) {
      let res = '';
      let chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
      for (let i = 0; i < length; i++) {
        res += chars.charAt(Math.floor(this.random(seed++) * chars.length));
      }
      return res;
    },
    stringToSeed(str) {
      return Array.from(str).map(c => c.charCodeAt(0)).reduce((a, b) => a + b, 0);
    },
    random(seed) {
      var x = Math.sin(seed) * 10000;
      return x - Math.floor(x);
    }
  }
}
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
}

#app {
  height: 100%;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #f1f0ea;
  background: rgb(28,28,28);
  background: linear-gradient(90deg, rgba(28,28,28,1) 0%, rgba(39,40,60,1) 35%, rgba(53,66,69,1) 100%);
  overflow: auto;
}

.logo {
  margin: 60px auto 0;
  width: 200px;
}

.form {
  margin: 50px auto 0;
  max-width: 700px;
}

.form-item {
  display: flex;
  flex-direction: column;
  margin-top: 28px;
}

label {
  margin-bottom: 8px;
  font-size: 16px;
  font-weight: 700;
  text-transform: uppercase;
}

input {
  padding: 10px 15px;
  border-radius: 10px;
  border: 3px solid #a86036;
  background: transparent;
  color: #f1f0ea;
  font-size: 16px;
  text-align: center;
}

input[type=number]
{
  -moz-appearance: textfield;
}

.result-box {
  margin-top: 50px;
}

.result {
  background: #00000033;
  border-radius: 10px;
  padding: 30px;
  word-break: break-all;
}
</style>
