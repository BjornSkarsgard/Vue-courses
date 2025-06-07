<script setup lang="ts">

import {ref, watch} from "vue";

interface ModalCard {
    id: number;
    title: string;
    des: string;
    duration: string;
    isActive: boolean;
}

const props = defineProps<{
    modal: ModalCard | null
}>()

const emit = defineEmits(['save'])
const editedCard = ref<ModalCard | null>(null)

watch(() => props.modal, (newVal) => {
    if (newVal) {
        editedCard.value = {...newVal}
    }
})

const save = () => {
    if (editedCard.value) {
        emit("save", editedCard.value);
    }
};
</script>

<template>
    <div id="modal-example" uk-modal>
        <div class="uk-modal-dialog uk-modal-body" v-if="editedCard">
            <h2 class="uk-modal-title">Редактирование курса</h2>
            <div class="uk-grid uk-child-width-1-1" uk-grid>
                <div>
                    <p class="uk-margin-xsmall-bottom">Название курса</p>
                    <input class="uk-input" type="text" v-model="editedCard.title">
                </div>
                <div>
                    <p class="uk-margin-xsmall-bottom">Описание курса</p>
                    <input class="uk-input" type="text" v-model="editedCard.des">
                </div>
                <div>
                    <p class="uk-margin-xsmall-bottom">Длительность курса</p>
                    <input class="uk-input" type="number" v-model="editedCard.duration">
                </div>
                <div>
                    <p class="uk-margin-xsmall-bottom">Доступность курса</p>
                    <label style="cursor: pointer">
                        <input class="uk-checkbox uk-margin-small-right" type="checkbox" v-model="editedCard.isActive">
                        <span class="uk-text-success" :class="editedCard.isActive ? 'uk-text-success' : 'uk-text-warning' ">{{ editedCard.isActive ? 'Доступен':'Не доступен' }}</span>
                    </label>
                </div>
            </div>

            <p class="uk-text-right">
                <button class="uk-button uk-button-default uk-modal-close" type="button">Отменить</button>
                <button class="uk-button uk-button-primary" type="button" @click="save">Сохранить</button>
            </p>
        </div>
    </div>
</template>

<style scoped>

</style>