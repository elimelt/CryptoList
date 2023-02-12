<template>
    <div class="settings-popup">
        <div class="settings-popup__body">
            <h3>Toggle Theme</h3>
            <div class="settings-popup__option">
                <label class="switch">
                    <input type="checkbox" v-model="isDark" @change="updateTheme" />
                    <span class="slider round"></span>
                </label>
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
            isDark: false
        }
    },
    methods: {
        updateTheme() {
            document.body.classList.toggle('dark-mode');
        },
        closeSettings() {
            this.$emit('closeSettings');
        }
    }
}
</script>
  

<style>
.settings-popup {
    display: flex;
    flex-direction: column;
    background-color: #fff;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    padding: 20px;
    z-index: 11;
    max-width: 300px;
    text-align: center;
}

.settings-popup__header {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 20px;
}

.settings-popup__body {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 20px;
}

.settings-popup__option {
    display: flex;
    align-items: center;
    margin-bottom: 20px;
}

.settings-popup__label {
    font-size: 14px;
    font-weight: 600;
    margin-right: 10px;
}

.switch {
    display: inline-block;
    width: 42px;
    height: 22px;
    border-radius: 22px;
    background-color: #ccc;
    position: relative;
    transition: background-color 0.3s;
}

.slider {
    position: absolute;
    top: 2px;
    bottom: 2px;
    left: 2px;
    right: 2px;
    border-radius: 20px;
    background-color: #fff;
    transition: all 0.3s;
}

input:checked+.slider {
    background-color: #2196F3;
}

input:checked+.slider:before {
    transform: translateX(18px);
}

input:checked+.switch {
    background-color: #2196F3;
}

.slider:before {
    content: '';
    position: absolute;
    width: 16px;
    height: 16px;
    border-radius: 50%;
    top: 3px;
    left: 3px;
    transition: all 0.3s;
}

.dark-mode .settings-popup {
    background-color: #333;
    color: #fff;
}

.dark-mode .settings-popup__body {
    border-bottom: 1px solid #555;
}

.dark-mode .slider {
    background-color: #fff;
}

.dark-mode input:checked+.slider {
    background-color: #fff;
}

.dark-mode input:checked+.switch {
    background-color: #fff;
}

.dark-mode .slider:before {
    background-color: #333;
}

.settings-popup__close-button {
    background-color: #2196F3;
    color: #fff;
    padding: 10px 20px;
}

.settings-popup__close-button:hover {
    background-color: #d6a03a6c;
    color: #fff;
}

.dark-mode .settings-popup__close-button:hover {
    background-color: #555;
}
</style>

