<template>
    <canvas ref="canvas" class="snow-canvas" aria-hidden="true"></canvas>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const props = defineProps({
    count: { type: Number, default: 150 },
    color: { type: String, default: '#ffffff' },
})

const canvas = ref(null)
let ctx = null
let width = 0
let height = 0
let flakes = []
let rafId = null

function resize() {
    const dpr = window.devicePixelRatio || 1
    width = window.innerWidth
    height = window.innerHeight
    const c = canvas.value
    if (!c) return
    c.width = Math.round(width * dpr)
    c.height = Math.round(height * dpr)
    c.style.width = width + 'px'
    c.style.height = height + 'px'
    ctx && ctx.setTransform(dpr, 0, 0, dpr, 0, 0)
}

function rand(min, max) {
    return Math.random() * (max - min) + min
}

function initFlakes() {
    flakes = []
    for (let i = 0; i < props.count; i++) {
        flakes.push({
            x: Math.random() * width,
            y: Math.random() * height,
            r: rand(0.6, 3.5),
            d: rand(0.5, 1.5),
            vx: rand(-0.5, 0.5),
        })
    }
}

function update() {
    if (!ctx) return
    ctx.clearRect(0, 0, width, height)
    ctx.fillStyle = props.color
    ctx.beginPath()
    for (let i = 0; i < flakes.length; i++) {
        const f = flakes[i]
        ctx.moveTo(f.x, f.y)
        ctx.arc(f.x, f.y, f.r, 0, Math.PI * 2)
        f.y += f.d + f.r * 0.3
        f.x += f.vx
        if (f.y > height + 5) {
            f.y = -10
            f.x = Math.random() * width
        }
        if (f.x > width + 5) f.x = -5
        if (f.x < -5) f.x = width + 5
    }
    ctx.fill()
    rafId = requestAnimationFrame(update)
}

onMounted(() => {
    const c = canvas.value
    if (!c) return
    ctx = c.getContext('2d')
    resize()
    initFlakes()
    window.addEventListener('resize', resize)
    rafId = requestAnimationFrame(update)
})

onUnmounted(() => {
    window.removeEventListener('resize', resize)
    if (rafId) cancelAnimationFrame(rafId)
})
</script>

<style scoped>
.snow-canvas {
    position: fixed;
    inset: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;
    z-index: 9999;
    mix-blend-mode: normal;
}
</style>
