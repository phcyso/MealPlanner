<script setup lang="ts">
import { useDataStore } from '../data/store';
import { XMarkIcon } from '@heroicons/vue/24/outline';


const store = useDataStore()
if (store.allIngredients.length == 0) { store.fetchIngredients() }

</script>
<template>
    <div class="card">
        <ul>
            <li v-for="ing in store.allIngredients">
                <div class="item-div"><span class="item">{{ ing.ingredientName }}</span>
                    <XMarkIcon @click="store.pushDeleteIngredient(ing)" class="del">
                    </XMarkIcon>
                </div>
            </li>
        </ul>
    </div>
</template>
<style scoped>
.item-div {
    display: flex;
    min-width: 200px;
    max-width: 40%;
}

.item {
    min-width: 100px;
    flex-grow: 2;
}

.edit {
    color: rgb(95, 52, 213);
    max-width: 1.5rem;
}

.del {
    color: crimson;
    max-width: 1.5rem;
}
</style>