<template>
    <div class="slider-container">
        <h1>Estou de férias! FLW!</h1>
        <h2>Até a volta!!!</h2>
        <h2>Abaixo um resumo do que farei...hehehehhe</h2>
        <Swiper :modules="modules" effect="cards" grab-cursor :pagination="{ clickable: true }" class="swiper">
            <SwiperSlide v-for="(item, index) in slides" :key="index" class="swiper-slide">
                <div class="card">
                    <img :src="item.image" :alt="item.title" class="card-image" />
                    <div class="card-content">
                        <h2>{{ item.title }}</h2>
                        <p>{{ item.description }}</p>
                    </div>
                </div>
            </SwiperSlide>
        </Swiper>
    </div>
</template>

<script setup>
import { Swiper, SwiperSlide } from 'swiper/vue'
import { EffectCards, Pagination } from 'swiper/modules'
import 'swiper/css'
import 'swiper/css/effect-cards'
import 'swiper/css/pagination'

const modules = [EffectCards, Pagination]

const slides = [
    {
        title: '1: Descansar a mente e o corpo',
        description: 'Tempo para relaxar e recarregar as energias.',
        image: 'https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExZW12YmZtdzhyY3ptZ3lnamNkNzdkcjluaXozMzlwZDZvZGs5b3l4ZiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/mkhMTALnrYRLnuoe5P/giphy.gif'
    },
    {
        title: '2: Estudar VR',
        description: 'Explorar novos conhecimentos e habilidades.',
        image: 'https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExc2M4cTV4Nzk0dmh1bHFrNWk2Y3l4OXE3OXp3anVrbG90dzduNXd6YiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/1uyFaGpt2ilmE/giphy.gif'
    },
    {
        title: '3: Se exercitar fisicamente',
        description: 'Sair da zona de conforto e cuidar do corpo.',
        image: 'https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExeGtjcnJmZDMwcjEzYzM5czMyZDBtejVtNnRtemJ5b3ZlZnNqODB4NiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/ccovgv47rJFHa/giphy.gif'
    },
    {
        title: '4: Exames e consultas médicas',
        description: 'Correr atrás das negligencias durantes esses anos',
        image: 'https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExeWFmczJuaGlveXQzdHNid3BxdGtkYWlsZG1hdnhsazBtcGJyOHkzdyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/KAkaqbTNnZ7bPiWdzZ/giphy.gif'
    },
    {
        title: '5: Fortal City',
        description: 'Contemplar o pôr do sol na melhor cidade Praiana do Brasil. Viva a energia vibrante de Fortaleza!',
        image: 'https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExeG80YmhrczY0N2ZrYndhZ2sxYW5kN3ZvaTZpeXhkZHd0YmVhcTNxaSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/mDSGaOdQxzdseSPdAi/giphy.gif'
    },
    {
        title: '6: Comemorar Natal',
        description: 'Melhor época festiva do ano, cheia de luzes, amor e esperança. Celebre o espírito natalino com quem você ama.',
        image: 'https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExcmRuem1xZnpxaGM3N21lM3BsczJxODQ0bmRwcmIyamNlN2xmbmF2eSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/3oriOb1AHvsIj24On6/giphy.gif'
    },
    {
        title: '7: Ano novo com estilo e volta ao trabalho',
        description: 'Que boas vibrações venham para conquistas e sucesso em 2026!',
        image: 'https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExeHZ1OHludmE4dXh4eTdrMWZ2MmV2anh6ZTE0ZDN3MTU1dnN2amc0byZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/QMkPpxPDYY0fu/giphy.gif'
    }
]
</script>

<style scoped>
.slider-container {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 2rem 1rem;
    position: relative;
    z-index: 10;
}

.swiper {
    width: 100%;
    max-width: 600px;
    height: 500px;
    padding-top: 20px;
}

.card {
    width: 100%;
    height: 100%;
    border-radius: 20px;
    overflow: hidden;
    box-shadow: 0 8px 30px rgba(0, 0, 0, 0.3);
    display: flex;
    flex-direction: column;
    position: relative;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

/* Different backgrounds per slide (valid CSS selectors) */
.swiper-slide:nth-child(1) .card {
    background: linear-gradient(135deg, #06fd50 0%, #0bd6aa 100%);
}

.swiper-slide:nth-child(2) .card {
    background: linear-gradient(135deg, #fd0606 0%, #d66d0b 100%);
}

.swiper-slide:nth-child(3) .card {
    background: linear-gradient(135deg, #06a6fd 0%, #0bd6ff 100%);
}

.swiper-slide:nth-child(4) .card {
    background: linear-gradient(135deg, #8e44ad 0%, #3498db 100%);
}

.swiper-slide:nth-child(5) .card {
    background: linear-gradient(135deg, #fffb00 0%, #ff7b00 100%);
}

.swiper-slide:nth-child(6) .card {
    background: linear-gradient(135deg, #e74c3c 0%, #c0392b 100%);
}

.swiper-slide:nth-child(7) .card {
    background: linear-gradient(135deg, #2778ae 0%, #652ecc 100%);
}

.card-image {
    width: 100%;
    height: 60%;
    object-fit: cover;
}

.card-content {
    height: 40%;
    padding: 1.5rem;
    color: white;
    display: flex;
    flex-direction: column;
    background: rgba(0, 0, 0, 0.3);
}

.card-content h2 {
    margin: 0;
    font-size: 1.5rem;
    font-weight: bold;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

.card-content p {
    margin: 0.5rem 0 0 0;
    font-size: 0.95rem;
    line-height: 1.4;
    text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.5);
}

:deep(.swiper-pagination-bullet) {
    background-color: rgba(255, 255, 255, 0.7);
}

:deep(.swiper-pagination-bullet-active) {
    background-color: white;
}

@media (min-width: 768px) {
    .swiper {
        max-width: 700px;
        height: 550px;
    }

    .card-content h2 {
        font-size: 1.8rem;
    }

    .card-content p {
        font-size: 1rem;
    }
}

@media (max-width: 1024px) {
    .slider-container {
        text-align: center;
    }
}
</style>
