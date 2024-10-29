<template>
  <div class="greetings">
    <h1>
      Faltam <span class="green">{{ message }}</span> segundos para as MINHAS
      FÉRIAS!
    </h1>
    <img
      width="220"
      height="220"
      src="https://cdn-icons-png.flaticon.com/512/2960/2960641.png"
      alt="Sol e Praia"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      date: new Date(),
      message: '',
    }
  },
  methods: {
    DateForVocation() {
      let vocation = new Date(this.date.getFullYear(), 11, 16)

      if (this.date > vocation) {
        vocation = new Date(this.date.getFullYear() + 1, 11, 16)
      }

      const differ = vocation - new Date()

      const day = Math.floor(differ / (1000 * 60 * 60 * 24))
      const hour = Math.floor(
        (differ % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60),
      )
      const minutes = Math.floor((differ % (1000 * 60 * 60)) / (1000 * 60))
      const seconds = Math.floor((differ % (1000 * 60)) / 1000)

      this.message = `${day} dias e ${hour < 10 ? '0' + hour : hour}:${minutes < 10 ? '0' + minutes : minutes}:${seconds < 10 ? '0' + seconds : seconds}`
    },
    updateCount() {
      this.DateForVocation()
      requestAnimationFrame(this.updateCount)
    },
  },
  mounted() {
    this.updateCount()
  },
}
</script>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 3.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
