<template>
  <div class="container">
    <h1>Kalkulator Konversi Waktu</h1>
    <div class="input-container">
      <label for="time">Masukkan Waktu (detik):</label>
      <input type="text" v-model="inputTime" @input="convertTime">
    </div>
    <div class="output-container">
      <h2>Hasil Konversi:</h2>
      <ul class="conversion-list">
        <li v-for="(value, unit) in convertedTime" :key="unit">{{ formatNumber(value) }} {{ unit }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      inputTime: '',
      convertedTime: {}
    };
  },
  methods: {
    convertTime() {
      const inputValue = parseFloat(this.inputTime);
      if (!isNaN(inputValue)) {
        this.convertedTime = {
          'jam': (inputValue / 3600),
          'menit': (inputValue / 60),
          'detik': inputValue,
          'milidetik': inputValue * 1000
        };
      } else {
        this.convertedTime = {};
      }
    },
    formatNumber(value) {
      // Menghilangkan dua nol di belakang titik desimal
      return parseFloat(value).toFixed(2).replace(/\.?0*$/, '');
    }
  }
};
</script>

<style scoped>
.container {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border-radius: 10px;
  background-color: #f0f0f0; /* Ubah warna latar belakang menjadi abu-abu */
  text-align: center;
  color: #333; /* Ubah warna teks menjadi gelap agar mudah terbaca */
  font-family: 'Times New Roman', Times, serif; /* Gunakan font Times New Roman */
}

h1 {
  font-size: 36px;
  margin-bottom: 20px;
}

.input-container {
  margin-bottom: 20px;
}

.input-container label {
  display: block;
  margin-bottom: 10px;
  font-size: 20px;
}

.input-container input {
  width: 80%;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  font-size: 18px;
}

.output-container {
  text-align: left;
}

.conversion-list {
  padding: 0;
  list-style-type: none;
}

.conversion-list li {
  margin-bottom: 10px;
  font-size: 20px;
}
</style>
