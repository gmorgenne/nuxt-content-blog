<script setup>

const toggleTheme = () => {
    const activeTheme = localStorage.getItem("user-theme");
    if (activeTheme === "light-theme") {
        setTheme("dark-theme");
    } else {
        setTheme("light-theme");
    }
}

const getTheme = () => {
    if (!process.client) {
        return "light-theme";
    }
    if (localStorage.getItem("user-theme")) {
        return localStorage.getItem("user-theme");
    }
    const hasDarkPreference = window.matchMedia("(prefers-color-scheme: dark)").matches;
    if (hasDarkPreference) {
        return "dark-theme";
    }
    return "light-theme";
}

const setTheme = (theme) => {
    if (process.client) {
        localStorage.setItem("user-theme", theme);
        document.documentElement.className = theme;
    }
    userTheme = theme;
}

let userTheme = getTheme() || "light-theme";
setTheme(userTheme);
</script>

<template>
    <div class="theme-button">
        <input @change="toggleTheme" id="checkbox" type="checkbox" class="switch-checkbox" />
        <label for="checkbox" class="switch-label">
            <span>🌙</span>
            <span>☀️</span>
            <div :class="userTheme === 'dark-theme' ? 'switch-toggle-checked' : 'switch-toggle' "></div>
        </label>
    </div>
</template>

<style scoped>
.theme-button {
    margin-top: 2px;
}
.switch-checkbox {
    display: none;
}

.switch-label {
    align-items: center;
    border-radius: 40px;
    cursor: pointer;
    display: flex;
    font-size: 12px;
    height: 22px;
    position: relative;
    padding: 4px;
    transition: background 0.5s ease;
    justify-content: space-between;
    width: 48px;
    z-index: 1;
}
.light-theme .switch-label {
    background: white;
    border: calc(40px * 0.025) solid black;
}

.dark-theme .switch-label {
    background: black;
    border: calc(40px * 0.025) solid white;
}

.switch-toggle {
    position: absolute;
    border-radius: 50%;
    top: 2px;
    left: 4px;
    height: 16px;
    width: 16px;
    transform: translateX(0);
    transition: transform 0.3s ease, background-color 0.5s ease;
}

.light-theme .switch-toggle {
    background-color: white;
    border: calc(40px * 0.025) solid black;
}

.dark-theme .switch-toggle {
    background-color: black;
    border: calc(40px * 0.025) solid white;
    transform: translateX(calc(40px * 0.6)) !important;
}
</style>