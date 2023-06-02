<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
  </header>
  <main>
    <h1>Warp engine</h1>
    <form @submit.prevent="onSubmit">
      <div>
        <label for="userName">Name</label>
        <input v-model="user.name" id="userName" type="text" placeholder="Name" />
      </div>
      <div>
        <label for="userEmail">E-mail</label>
        <input v-model="user.email" id="userEmail" type="email" placeholder="E-mail" />
      </div>
      <input type="submit" value="Start" />
    </form>
    <button @click="stopEngine">Stop</button>
    <div>{{ engineState }}</div>
    <table v-if="statuses.length">
      <tr>
        <th>Date</th>
        <th>Seconds elapsed</th>
        <th>Flow rate</th>
        <th>Intermix</th>
        <th>Matter adjustment</th>
        <th>Antimatter adjustment</th>
      </tr>
      <StatusRow v-for="status in statuses" :status="status" />
    </table>
  </main>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import StatusRow from '@/components/StatusRow.vue';

const API_URL = 'http://localhost:3000'

const user = {
  name: "Juhan Juurikas",
  email: "juhan@example.com"
}

const engineState = ref('')
const statuses = ref([])
let intervalId = 0

const onSubmit = async () => {
  const startResponse = await fetch(API_URL + '/start', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(user)
  })

  const startData = await startResponse.json()
  engineState.value = startData.message

  if (startData) {
    intervalId = setInterval(async () => {
      const statusResp = await fetch(API_URL + '/status')
      const status = await statusResp.json()
      statuses.value.unshift(status)
      engineState.value = status.engineState
    }, 1000)
  }
}

const stopEngine = async () => {
  const stopResponse = await fetch(API_URL + '/stop', {
    method: 'POST'
  })
  const stopData = await stopResponse.json()
  engineState.value = stopData.message
  clearInterval(intervalId)
}

</script>

<style scoped>
label {
  margin-right: 0.5rem;
}
</style>
