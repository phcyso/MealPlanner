<script setup lang="ts">
import { ref } from 'vue';
import ModalComp from './ModalComp.vue';
import { MealPlan } from '../data/types';
import MealPlanForm from './MealPlanForm.vue';
import { PlusCircleIcon, PencilSquareIcon } from '@heroicons/vue/24/outline';
import LoadingWheel from './LoadingWheel.vue';

const props = defineProps<{
    plan: MealPlan
}>()

// modal controls
const isModalOpened = ref(false);

const openModal = () => {
    isModalOpened.value = true;
};
const closeModal = () => {
    isModalOpened.value = false;
};

const submitHandler = () => {
    closeModal()
}
</script>
<template>
    <PlusCircleIcon v-if="!props.plan.dinner" @click="openModal" class="addEditMeal"></PlusCircleIcon>
    <PencilSquareIcon v-else @click="openModal" class="addEditMeal"></PencilSquareIcon>
    <ModalComp :isOpen="isModalOpened" @modal-close="closeModal" @submit="submitHandler" name="first-modal">
        <template #header>
            <h3>Meal Allocation - {{ props.plan.day }}</h3>
        </template>
        <template #content>
            <Suspense>
                <MealPlanForm v-bind="props.plan"></MealPlanForm>
                <template #fallback>
                    <LoadingWheel />
                </template>
            </Suspense>
        </template>
        <template #footer></template>
    </ModalComp>
</template>

<style scoped>
.addEditMeal {
    color: rgb(95, 52, 213);
    max-width: 1.5rem;
}
</style>