<template>
    <div class="settings-popup">
      <div class="settings-popup__body">
        <h3>Choose a theme</h3>
        <div class="settings-popup__option">
          <input type="radio" id="light" value="light" v-model="selectedTheme" @click="updateTheme('light')"/>
          <label for="light">Light</label>
        </div>
        <div class="settings-popup__option">
          <input type="radio" id="dark" value="dark" v-model="selectedTheme" @click="updateTheme('dark')"/>
          <label for="dark">Dark</label>
        </div>
      </div>
      <button class="settings-popup__close-button" @click="closeSettings">Close</button>
    </div>
  </template>
  
  <script>
  export default {
    name: 'SettingsPopup',
    data() {
      return {
        selectedTheme: 'light'
      }
    },
    methods: {
      updateTheme(theme) {
        document.body.className = theme;
        this.selectedTheme = theme;
      },
      closeSettings() {
        this.$emit('closeSettings');
      }
    }
  }
  </script>
  