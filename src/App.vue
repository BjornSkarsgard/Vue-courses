<script setup>
    import {ref} from "vue";
    import AppCourses from "@/components/AppCourses.vue";
    import AppModal from "@/components/AppModal.vue";

    const selectedCard = ref(null)
    let cards = ref([])
    const cardsIsLoading = ref(true)
    const isSaving = ref(false);

    const handleCardClick = (card) => {
        selectedCard.value = card
        UIkit.modal('#modal-example').show();
    }

    const handleSaveCard = (updatedCard) => {
        isSaving.value = true

        UIkit.modal("#modal-example").hide();

        setTimeout(() => {
            const index = cards.value.findIndex((c) => c.id === updatedCard.id);
            if (index !== -1) {
                cards.value.splice(index, 1,{ ...updatedCard });
            }
            isSaving.value = false;
        }, 2000);
    };
    const loadCards = () => {
        setTimeout(() => {
            cards.value = [
                {
                    title: 'Python-разработка',
                    des: 'Освой язык программирования Python с нуля: синтаксис, работа с данными, API и автоматизация задач.',
                    duration: '40',
                    isActive: true,
                    id: 1,
                },
                {
                    title: 'UI/UX-дизайн',
                    des: 'Научись проектировать интерфейсы, которые удобны и красивы. Figma, прототипы, работа с заказчиком.',
                    duration: '35',
                    isActive: true,
                    id: 2,
                },
                {
                    title: 'Веб-разработка (HTML, CSS, JS)',
                    des: 'Создавай современные сайты и лендинги. От базовой вёрстки до интерактива на JavaScript.',
                    duration: '50',
                    isActive: true,
                    id: 3,
                },
                {
                    title: 'Кибербезопасность',
                    des: 'Погружение в мир информационной безопасности: защита данных, атаки и методы противодействия.',
                    duration: '45',
                    isActive: false,
                    id: 4,
                },
                {
                    title: 'DevOps-инженер',
                    des: 'Изучи CI/CD, Docker, Kubernetes и настрой автоматизацию для современных IT-проектов.',
                    duration: '60',
                    isActive: true,
                    id: 5,
                },
                {
                    title: 'Data Science и машинное обучение',
                    des: 'Работа с данными, Pandas, NumPy, модели машинного обучения и практика на Python.',
                    duration: '70',
                    isActive: true,
                    id: 6,
                },
                {
                    title: 'Продакт-менеджмент в IT',
                    des: 'Как управлять цифровыми продуктами, Agile, Scrum, MVP и анализ рынка.',
                    duration: '30',
                    isActive: false,
                    id: 7,
                },
                {
                    title: 'Мобильная разработка',
                    des: 'Разработка приложений на Flutter и React Native. Публикация в App Store и Google Play.',
                    duration: '55',
                    isActive: true,
                    id: 8,
                }
            ]

            cardsIsLoading.value = false

        }, 2000)
    }

    loadCards()
</script>


<template>
    <div class="uk-container uk-container-xlarge">
        <h1 class="uk-text-bold">Список курсов</h1>

        <app-courses v-if="!cardsIsLoading && !isSaving" :cards="cards" @card-clicked="handleCardClick"/>

        <div v-else class="uk-width-1-1 uk-flex uk-flex-center uk-flex-middle uk-height-viewport">
            <img  src="/load.gif" alt="" width="100" height="100">
        </div>
    </div>

    <app-modal :modal="selectedCard" @save="handleSaveCard"/>
</template>

<style scoped>

</style>
