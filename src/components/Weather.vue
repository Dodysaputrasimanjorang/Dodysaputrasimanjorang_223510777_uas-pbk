<template>
  <div class="weather-container q-pa-md">
    <div class="form-container">
      <h4 class="q-mb-md form-title">Aplikasi Cuaca</h4>
      <form @submit.prevent="getCuaca" class="q-gutter-md form-inline">
        <q-input
          outlined
          square
          v-model="kota"
          label="Masukkan kota"
          autofocus
          class="form-input"
        />
        <q-btn
          square 
          type="submit"
          color="grey"
          icon="search"
          class="form-button"
          size="21px"
        />
      </form>
    </div>



    <p v-if="!sedangMemuat && !dataCuacaAda" class="q-mt-lg"></p>

    
    <div v-if="dataCuacaAda && !sedangMemuat" class="q-mt-lg weather-info">
      <p>Cuaca Saat Ini: {{ cuacaSaatIni }}</p>
      <p>Suhu: {{ suhu }}°C</p>
      <p>Kecepatan Angin: {{ kecepatanAngin }} m/s</p>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import axios from 'axios';

export default {
  name: 'Weather',
  setup() {
    const kota = ref(''); 
    const sedangMemuat = ref(false); 
    const dataCuacaAda = ref(false);
    const cuacaSaatIni = ref(''); 
    const suhu = ref(0); 
    const kecepatanAngin = ref(0); 

    
    const getCuaca = async () => {
      sedangMemuat.value = true; 
      dataCuacaAda.value = false; 
      const apiKey = '36d63746096ffc0326aacb289eb0d724'; 
      
      const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${kota.value}&appid=${apiKey}&units=metric`;
      
      try {
        const response = await axios.get(apiUrl);
        const data = response.data;
        cuacaSaatIni.value = data.weather[0].description;
        suhu.value = data.main.temp;
        kecepatanAngin.value = data.wind.speed;
        dataCuacaAda.value = true; 
        
        
        setTimeout(() => {
          sedangMemuat.value = false; 
        }, 2000);
        
      } catch (error) {
        console.error('Error fetching weather data:', error);
        sedangMemuat.value = false; 
      }
    };

    return {
      kota,
      sedangMemuat,
      dataCuacaAda,
      cuacaSaatIni,
      suhu,
      kecepatanAngin,
      getCuaca
    };
  }
}
</script>

<style scoped>
.weather-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
  font-family: 'Arial', sans-serif;
}

.form-container {
  width: 100%;
  max-width: 400px;
  background: #f0f0f0;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.form-title {
  text-align: center;
  font-size: 24px;
  font-weight: bold;
  color: #333;
  margin-bottom: 20px;
}

.form-inline {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 16px;
}

.form-button {
  margin-left: 10px;
  padding: 10px 20px;
  background-color: #4CAF50;
  color: #fff;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.form-button:hover {
  background-color: #45a049;
}

.weather-info {
  background: #333;
  color: #fff;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 1 4px 8px rgba(208, 9, 9, 0.1);
  max-width: 400px;
  width: 100%;
  text-align: center;
  margin-top: 20px;
  font-size: 18px;
}

.weather-info h2 {
  margin: 0 0 10px;
  font-size: 24px;
}

.weather-info p {
  margin: 5px 0;
}

</style>
