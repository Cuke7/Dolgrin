<template>
    <div class="flex flex-col bg-primary rounded-lg bg-opacity-20 p-2">
        <div>
            Nom : <span class="text-primary font-bold">{{ character.nom }}</span>
        </div>
        <div>
            Classe : <span class="text-primary font-bold">{{ character.classe }}</span>
        </div>
        <div>
            héritage : <span class="text-primary font-bold">{{ character.race }}</span>
        </div>
        <div>
            Alignement : <span class="text-primary font-bold">{{ character.alignement }}</span>
        </div>
        <div>
            Langues : <span v-for="langue in character.langues" class="text-primary font-bold whitespace-pre">{{ langue + " " }} </span>
        </div>
        <div>
            Taille : <span class="text-primary font-bold">{{ character.taille }}</span>
        </div>
        <div>
            Vitesse : <span class="text-primary font-bold">{{ character.VD }}{{ character.VD ? "m" : "" }}</span>
        </div>
        <div>
            Réserve focalisation : <span class="text-primary font-bold">{{ character.focal }}</span>
        </div>
    </div>
</template>

<script lang="ts" setup>
const props = defineProps(["character"]);
</script>
