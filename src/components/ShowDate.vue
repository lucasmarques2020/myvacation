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
      :src="srcImage"
      alt="Sol e Praia"
    />
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const message = ref('')
let srcImage = ref('./src/assets/bg-vacation.webp')
const emit = defineEmits(['vacation-started'])
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

  // Check if vacation has started (day <= 0)
  if (day <= 0 && hour === 0 && minutes === 0 && seconds === 0) {
    emit('vacation-started')
    message.value = 'FÉRIAS COMEÇARAM! 🎉'
  } else {
    message.value = `${day} dias e ${hour < 10 ? '0' + hour : hour}:${minutes < 10 ? '0' + minutes : minutes}:${seconds < 10 ? '0' + seconds : seconds}`
  }

  if(day < 5) {
    document.querySelector('body').classList.add('urgent');
    srcImage = 'https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExOTU0MjZicnVvbHJybnQ1cDVqcGNkdHR4Z2t4dTFzZGdzN3psdGFidSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/wuOtkQMVrqdRS/giphy.gif';
  }

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

.urgent {
  span {
    color: #a10000;
    fill: white;
    text-shadow: 0 0 5px rgb(255, 255, 255);
  }
  h1 {
    color: #ff0101;
    fill: white;
    text-shadow: 0 0 5px rgb(255, 255, 255);
    animation: infinite 1s pulse alternate;
  }
}

@keyframes pulse {
  from {
    transform: scale(1);
  }
  to {
    transform: scale(1.1);
  }
}
</style>
