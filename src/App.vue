<template>
  <div class="q-pa-none">
    <q-layout>
      <q-header elevated class="bg-grey">
        <q-toolbar inset></q-toolbar>
        <q-toolbar>
          <q-toolbar-title>
            <strong>Weather App</strong> 
          </q-toolbar-title>
          <q-btn-dropdown color="dark" label="TUGAS">
            <q-list>
              <q-item
                v-for="task in tasks"
                :key="task.name"
                clickable
                @click="openInNewTab(task.path)"
              >
                <q-item-section>{{ task.name }}</q-item-section>
              </q-item>
            </q-list>
          </q-btn-dropdown>
        </q-toolbar>
        <q-toolbar inset></q-toolbar>
      </q-header>

      <q-page-container>
        <q-page>
          <router-view></router-view>
        </q-page>
      </q-page-container>
    </q-layout>
  </div>
</template>

<script>
import Weather from './components/Weather.vue';

export default {
  name: 'App',
  components: {
    Weather,
  },
  data() {
    return {
      tasks: [
        { name: 'Tugas 1', path: 'https://pertemuan1-92b01.firebaseapp.com/' },
        { name: 'Tugas 2', path: 'https://223510777-tugas2.netlify.app/' },
        { name: 'Tugas 3', path: 'https://223510777-tugas3.netlify.app/' },
        { name: 'Tugas 4', path: 'https://dody-tugas4-pbk.netlify.app/' },
        { name: 'Tugas 5', path: 'https://dody-tugas5-pbk.netlify.app/' },
        { name: 'Tugas 6', path: 'https://dodyy-tugas6-pbk.netlify.app/' },
        { name: 'Tugas 7', path: 'https://dodyy-tugas7-pbk.netlify.app/' },
      ]
    };
  },
  methods: {
    openInNewTab(url) {
      window.open(url, '_blank');
    }
  }
}
</script>

<style scoped>
.weather-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
}

.form-container {
  width: 100%;
  max-width: 400px;
}

.form-title {
  text-align: center;
}

.form-inline {
  display: flex;
  align-items: center;
}

.form-input {
  flex: 1;
}

.form-button {
  margin-left: 8px;
}

.weather-info {
  background: #ffffff;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(208, 11, 11, 0.1);
  max-width: 400px;
  width: 100%;
  text-align: center;
}
</style>
