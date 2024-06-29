<template>
  <q-page class="background-image" padding>
    <div class="form-container">
      <q-form @submit.prevent="fetchApodData">
        <q-input
          filled
          v-model="startDate"
          label="Fecha Inicio"
          type="date"
          class="nasa-input"
        />
        <q-input
          filled
          v-model="endDate"
          label="Fecha Fin"
          type="date"
          class="nasa-input"
        />
        <q-btn
          type="submit"
          label="Consultar"
          color="primary"
          class="q-mt-md nasa-btn"
        />
      </q-form>
    </div>

    <div v-if="apodData.length" class="q-mt-lg">
      <q-card v-for="item in apodData" :key="item.date" class="q-mb-md">
        <q-card-section>
          <div class="text-h6">{{ item.title }}</div>
          <div class="text-subtitle2">{{ item.date }}</div>
        </q-card-section>
        <div v-if="item.media_type === 'image'">
          <q-img :src="item.url" :alt="item.title" ratio="16/9" />
        </div>
        <div v-else-if="item.media_type === 'video'">
          <iframe
            :src="item.url"
            frameborder="0"
            allow="autoplay; encrypted-media"
            allowfullscreen
          ></iframe>
        </div>
        <q-card-section>
          <p>{{ item.explanation }}</p>
        </q-card-section>
      </q-card>
    </div>
  </q-page>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      startDate: "",
      endDate: "",
      apodData: [],
      apiKey: "lPVl5bj2ns4FIm7p69EA5HLGaFZ0LIPTRTKPyJRG",
    };
  },
  methods: {
    async fetchApodData() {
      if (this.startDate && this.endDate) {
        try {
          const response = await axios.get(
            "https://api.nasa.gov/planetary/apod",
            {
              params: {
                api_key: this.apiKey,
                start_date: this.startDate,
                end_date: this.endDate,
              },
            }
          );
          console.log(response.data);
          this.apodData = response.data;
        } catch (error) {
          console.error(error);
        }
      } else {
        alert("Por favor, selecciona ambas fechas");
      }
    },
  },
};
</script>

<style scoped>
.q-card {
  max-width: 33%;
  margin: auto;
  padding: 18px;
  display: inline-grid;
}

iframe {
  width: 100%;
  height: 315px;
}

.background-image {
  background-image: url("/src/img/nasa-logo-web-rgb.jpg");
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  height: 100vh;
}

.form-container {
  background-color: rgba(255, 255, 255, 0.8);
  padding: 20px;
  border-radius: 8px;
  backdrop-filter: blur(10px);
  margin: auto;
  max-width: 600px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.nasa-input {
  background-color: transparent;
  border-color: #bcbcbc;
  color: #333;
  margin-right: 10px;
}

.nasa-btn {
  background-color: #0072cf;
  color: #fff;
  margin-top: 10px;
}
</style>
