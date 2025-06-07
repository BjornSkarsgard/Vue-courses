<script setup lang="ts">
    interface CourseCard {
        id: number;
        title: string;
        des: string;
        duration: string;
        isActive: boolean;
    }


    const props = defineProps<{
        index: number;
        card: CourseCard;
    }>()

    const emit = defineEmits<{
        (e: 'card-clicked', payload: CourseCard):void
    }>()

    const handleClick = () => {
        emit('card-clicked', props.card)
    }

    const calculated = function (months) {
        const years = Math.floor(months / 12);
        const remainingMonths = months % 12;

        const getYearWord = (num) => {
            if (num === 1) return "год";
            if (num >= 2 && num <= 4) return "года";
            return "лет";
        };

        const getMonthWord = (num) => {
            if (num === 1) return "месяц";
            if (num >= 2 && num <= 4) return "месяца";
            return "месяцев";
        };

        let result = [];

        if (years > 0) {
            result.push(`${years} ${getYearWord(years)}`);
        }

        if (remainingMonths > 0 || months === 0) {
            result.push(`${remainingMonths} ${getMonthWord(remainingMonths)}`);
        }

        return result.join(" ");
    }
</script>

<template>
    <div>
        <div @click="handleClick" class="uk-card uk-card-default uk-border-rounded uk-flex uk-flex-column" :class="{'uk-background-muted':!card.isActive}">
            <div class="uk-card-header uk-padding-small">
                <p class="uk-text-large" :class="{'uk-text-primary':card.isActive}">{{card.title}}</p>
            </div>
            <div class="uk-card-body uk-padding-small">
                <p :class="{'uk-text-secondary':card.isActive}">{{card.des}}</p>
            </div>
            <div v-if="card.isActive" class="uk-card-footer uk-padding-small">
                <p class="uk-label">{{calculated(Number(card.duration))}}</p>
            </div>

            <div class="uk-margin-auto-top" v-else>
                <p class="uk-label-warning uk-text-bolder uk-padding-small uk-border-rounded uk-margin-remove">К сожалению курс не доступен</p>
            </div>
        </div>
    </div>

</template>

<style scoped>

</style>