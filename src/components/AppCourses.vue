<script setup lang="ts">

import AppCard from "@/components/AppCard.vue";

interface CourseCard {
    id: number;
    title: string;
    des: string;
    duration: string;
    isActive: boolean;
}

const props = defineProps<{
    cards: CourseCard[]
}>()

const emit = defineEmits<{
    (e: 'card-clicked', payload: CourseCard):void
}>()

const handleClick = (card: CourseCard) => {
    emit('card-clicked', card)
}

</script>

<template>
    <div class="uk-grid uk-grid-small uk-child-width-1-3" uk-grid uk-height-match="target: * > .uk-card">
        <app-card
            v-for="(card, index) in cards"
            :key="card.id"
            :card="card"
            :index="index"
            @card-clicked="handleClick"
        />
    </div>
</template>

<style scoped>

</style>