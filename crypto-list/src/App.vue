<template>
  <body v-bind:class="{ 'dark-mode': isDark }">
    <div id="app">
      <SettingsPopup v-if="showSettings" @closeSettings="closeSettings"/>
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
  color: #6b7f94;
  font-weight: 500;
  margin-top: 60px;
}

.header {
  background-color: #ccc;
  height: 40px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  padding: 0 20px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
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

body.dark {
  background-color: #001;
}
</style>
