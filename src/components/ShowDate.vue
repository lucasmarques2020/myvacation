<template>
  <div class="greetings">
    <h1>
      Faltam <span>{{ message }}</span> para as minhas
      <span>FÉRIAS!</span>
    </h1>
    <img
      class="bg-vaction"
      width="220"
      height="220"
      src="../assets/bg-vacation.webp"
      alt="Sol e Praia"
    />
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const message = ref('')
let rafId = null

function updateMessage() {
  const now = new Date()
  let vocation = new Date(now.getFullYear(), 11, 6)

  if (now > vocation) {
    vocation = new Date(now.getFullYear() + 1, 11, 6)
  }

  const differ = vocation - now

  const day = Math.floor(differ / (1000 * 60 * 60 * 24))
  const hour = Math.floor((differ % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
  const minutes = Math.floor((differ % (1000 * 60 * 60)) / (1000 * 60))
  const seconds = Math.floor((differ % (1000 * 60)) / 1000)

  message.value = `${day} dias e ${hour < 10 ? '0' + hour : hour}:${minutes < 10 ? '0' + minutes : minutes}:${seconds < 10 ? '0' + seconds : seconds}`

  rafId = requestAnimationFrame(updateMessage)
}

onMounted(() => {
  updateMessage()
})

onUnmounted(() => {
  if (rafId) cancelAnimationFrame(rafId)
})
</script>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 3.6rem;
  position: relative;
  z-index: 1;
  font-size: 2.6rem;
  color: white;
}

.greetings {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.greetings h1 {
  text-align: center;
  font-weight: 500;
}

span {
  color:#e4cc21ff;
  font-weight: 900;
}

.bg-vaction {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

@media (min-width: 1024px) {
  .greetings h1 {
    text-align: left;
    top: -10rem;
    font-size: 3.6rem;
  }
}
</style>
