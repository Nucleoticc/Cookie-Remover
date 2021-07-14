<template>
  <div class="container">
    <div class="input-area">
      <label for="url">Current Site URL</label>
      <input type="text" name="url" placeholder=" " v-model="baseUrl" />
    </div>
    <div class="button-area">
      <button @click="clearCookies">Clear 🍪</button>
    </div>
  </div>
</template>

<script lang="ts">
import { ref, onMounted, defineComponent } from 'vue';

export default defineComponent({
  setup() {
    const fieldUrl = ref('');
    const baseUrl = ref('');

    const clearCookies = () => {
      chrome.cookies.getAll({ url: baseUrl.value }, function (cookies) {
        for (let i = 0; i < cookies.length; i++) {
          chrome.cookies.remove({
            url: baseUrl.value + cookies[i].path,
            name: cookies[i].name,
          });
        }
        chrome.tabs.reload();
      });
    };

    const getCurrentPageUrl = () => {
      chrome.tabs.query({ active: true, lastFocusedWindow: true }, (tabs) => {
        fieldUrl.value = tabs[0].url!;
        const data = fieldUrl.value.split('/');
        baseUrl.value = data[0] + '//' + data[2];
      });
    };

    onMounted(getCurrentPageUrl);

    return {
      baseUrl,
      clearCookies,
      getCurrentPageUrl,
    };
  },
});
</script>

<style scoped>
.container {
  height: 90%;
}

.input-area {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 80%;
  margin-left: 2rem;
  margin-right: 2rem;
}

.button-area {
  display: flex;
  justify-content: space-evenly;
}

input {
  width: 100%;
  margin-bottom: 2rem;
  font-size: 16px;
  border: none;
  border-bottom: 2px solid #111;
  text-align: center;
}

input:focus {
  outline: none;
  border-color: #dc143c;
}

button {
  width: 8rem;
  padding: 0.75rem 1.5rem;
  border: 2px solid #111;
  background-color: #111;
  color: #fff;
  font-weight: bold;
}
</style>
