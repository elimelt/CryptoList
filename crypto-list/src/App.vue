<template>
  <body v-bind:class="{ 'dark-mode': isDark }">
    <div id="app">
      <h1 class="title-heading">Crypto List</h1>
      <SettingsPopup isDark="isDark" v-if="showSettings" @closeSettings="closeSettings" />
      <div class="header">
        <button class="header-button" @click="toggleSettings">Settings</button>
      </div>
      <CryptoList />
    </div>
  </body>
</template>

<script>
import CryptoList from './components/CryptoList.vue'
import SettingsPopup from './components/SettingsPopup.vue'

export default {
  name: 'App',
  components: {
    CryptoList,
    SettingsPopup
  },
  data() {
    return {
      showSettings: false,
      isDark: false
    }
  },
  methods: {
    toggleSettings() {
      this.showSettings = !this.showSettings
    },
    closeSettings() {
      this.showSettings = false
    },
    toggleDarkMode() {
      this.isDark = !this.isDark
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #cca436;
  font-weight: 500;
  margin-top: 60px;
}

.title-heading {
  font-family: monospace;
  font-size: 50px;
  font-weight: bold;
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 2px;
  background-image: linear-gradient(to right, #ad6b09, #1600e0);
  color: #ffffff;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.25);
}


.header {
  background-color: #b97816f3;
  height: 40px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  padding: 0 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 10;
}

.header-button {
  background-color: transparent;
  border: none;
  outline: none;
  cursor: pointer;
  font-size: 16px;
  color: #333;
}

body.dark-mode {
  background-color: #001;
}
</style>

