<template>
  <header class="App-header">
    <img src="@/assets/logo-dark.svg" class="App-logo" alt="logo" />
    <p style="font-size: 2em; margin-bottom: 0.5em">Ready. Lets build the new web</p>
    <div
      style="display: flex; font-size: 0.7em; text-align: left; padding: 2em; border-radius: 30px; flex-direction: column; background: rgb(220 218 224 / 25%);">
      <div>
        <code>npm run dev:</code>
        <span> Runs the development server</span>
      </div>
      <div>
        <code>npm run build:</code>
        <span> Builds your frontend for production</span>
      </div>
      <div>
        <code>npm run serve:</code>
        <span> Serves your production-built frontend locally</span>
      </div>
      <hr />
      <div>
        <code>dfx deploy:</code>
        <span> Compiles & deploys your canisters</span>
      </div>
      <div style="text-align: center; font-size: 0.8em; margin-top: 2em;">
        <a
          class="App-link"
          href="https://vitejs.dev/guide/features.html"
          target="_blank"
          rel="noopener noreferrer"
        >
          Vite Docs
        </a>
        {{" | "}}
        <a
          class="App-link"
          href="https://sdk.dfinity.org/docs/developers-guide/sdk-guide.html"
          target="_blank"
          rel="noopener noreferrer"
        >
          IC SDK Docs
        </a>
      </div>
    </div>
    <button class="demo-button" @click="increment2()">
      Count is: {{ count2 }}
    </button>
    <p style="font-size: 0.6em;">
      This counter is running inside a canister
    </p>
    <p style="font-size: 0.4em;">by <a href="https://twitter.com/miamaruq">@miamaruq</a></p>
  </header>
</template>

<script lang="ts">
import { ref, onMounted } from "vue"
import { backend2 } from "canisters/backend2"

export default {
  name: "Intro",
  setup: () => {
    const count2 = ref(0)

    const refreshCounter2 = async () => {
      const res: any = await backend2.getValue()
      count2.value = res.toString()
    }

    const increment2 = async () => {
      await backend2.increment()
      refreshCounter2()
    }

    onMounted(refreshCounter2)

    return { increment2, count2 }
  },
}
</script>

<style scoped>
.App-logo {
  height: 15vmin;
  pointer-events: none;
}

.App-header {
  margin-top: 150px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
}

.App-link {
  color: rgb(26, 117, 255);
}

.demo-button {
  background: #a02480;
  padding: 0 1.3em;
  margin-top: 1em;
  border-radius: 60px;
  font-size: 0.7em;
  height: 35px;
  outline: 0;
  border: 0;
  cursor: pointer;
  color: white;
}

.demo-button:active {
  color: white;
  background: #979799;
}
</style>
