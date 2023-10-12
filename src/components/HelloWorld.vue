<template>
  <div>
    <h1>Cifrado César en Vue.js</h1>
    <div>
      <label for="message">Mensaje:</label>
      <input v-model="message" id="message" />
    </div>
    <div>
      <label for="shift">Desplazamiento:</label>
      <input v-model="shift" id="shift" />
    </div>
    <div>
      <button @click="encrypt">Cifrar</button>
      <button @click="decrypt">Descifrar</button>
    </div>
    <div>
      <p>Texto cifrado: {{ encryptedMessage }}</p>
      <p>Texto descifrado: {{ decryptedMessage }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: '',
      shift: 3, // Cambia el valor del desplazamiento según tus necesidades
      encryptedMessage: '',
      decryptedMessage: '',
    };
  },
  methods: {
    encrypt() {
      this.encryptedMessage = this.cesarCipher(this.message, this.shift);
    },
    decrypt() {
      this.decryptedMessage = this.cesarCipher(this.encryptedMessage, -this.shift);
    },
    cesarCipher(text, shift) {
      return text
        .split('')
        .map(char => {
          const charCode = char.charCodeAt(0);
          if (char.match(/[a-zA-Z]/)) {
            const offset = charCode >= 'a'.charCodeAt(0) ? 'a'.charCodeAt(0) : 'A'.charCodeAt(0);
            return String.fromCharCode(((charCode - offset + shift + 26) % 26) + offset);
          }
          return char;
        })
        .join('');
    },
  },
};
</script>