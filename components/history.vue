<template>
    <div class="flex flex-col">
        <div class="text-center mt-4 mb-2 border-b-2 border-primary mx-14">Autres compétences</div>
        <div v-for="autre in character.autres_competences" class="flex justify-between space-y-1">
            <span>
                {{ autre.nom }}
            </span>
            <maitrise :qual="autre.maitrise" :niveau="character.niveau" />
        </div>
    </div>
</template>

<script lang="ts" setup>
const props = defineProps(["character"]);
</script>
