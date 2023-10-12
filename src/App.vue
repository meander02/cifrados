<template>
  <div id="app">
    <h1>Cifrado César</h1>
    <div class="cifrado-container">
      <div class="input-container">
        <label for="inputTextEncrypt">Texto a cifrar:</label>
        <input style="color: blue;" v-model="inputTextEncrypt" id="inputTextEncrypt" class="custom-input"
          placeholder="Ingresa el texto a cifrar" />
      </div>
      <div class="input-container">
        <label for="inputTextDecrypt">Texto a descifrar:</label>
        <input style="color: rgb(43, 177, 63);" v-model="inputTextDecrypt" id="inputTextDecrypt" class="custom-input"
          placeholder="Ingresa el texto a descifrar" />
      </div>
      <div class="buttons-container">
        <button @click="encryptText" class="custom-button">Cifrar</button>
        <button @click="decryptText" class="custom-button">Descifrar</button>
      </div>
      <div class="resultado-container">
        <p style="color: blue;">Texto cifrado: {{ resultTextEncrypt }}</p>
        <p style="color: rgb(43, 177, 63);">Texto descifrado: {{ resultTextDecrypt }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputTextEncrypt: '',
      inputTextDecrypt: '',
      resultTextEncrypt: '',
      resultTextDecrypt: '',
    };
  },
  methods: {
    cesarCipher(input, shift) {
      let result = '';
      for (let i = 0; i < input.length; i++) {
        let char = input[i];
        if (char !== ' ') {
          let code = input.charCodeAt(i);
          code = (code - 97 + shift) % 26;
          if (code < 0) {
            code = 26 + code;
          }
          result += String.fromCharCode(code + 97);
        } else {
          result += ' ';
        }
      }
      return result;
    }
    ,
    encryptText() {
      const shift = 5; // Número de posiciones a desplazar
      this.resultTextEncrypt = this.cesarCipher(this.inputTextEncrypt, shift);
    },
    decryptText() {
      const shift = 5; // Número de posiciones a desplazar
      this.resultTextDecrypt = this.cesarCipher(this.inputTextDecrypt, -shift);
    },

  },
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  font-size: 2em;
  margin-bottom: 20px;
}

.cifrado-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
}

.input-container {
  text-align: left;
  margin: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 100%;
  max-width: 400px;
}

.input-container label {
  display: block;
  font-size: 1.2em;
  margin-bottom: 5px;
}

.custom-input {
  width: 80%;
  padding: 10px;
  font-size: 1em;
  border: none;
  border: 1px solid #3490dc;
  border-radius: 5px;
}

.buttons-container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 10px;
}

.custom-button {
  padding: 10px 20px;
  font-size: 1em;
  background-color: #3490dc;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.custom-button:hover {
  background-color: #2779bd;
}

.resultado-container {
  text-align: left;
}

@media (max-width: 768px) {
  .cifrado-container {
    margin: 20px;
  }
}
</style>