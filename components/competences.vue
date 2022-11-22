<template>
    <div class="flex flex-col w-1/2">
        <div class="flex text-[0.5rem] h-3">
            <span>COMPÉTENCE</span>
            <span class="ml-20 px-2">TOTAL</span>
            <span class="ml-5">MOD. CARA</span>
            <span class="ml-12">MAÎTRISE</span>
            <span class="ml-11">DIVERS</span>
        </div>
        <div class="flex justify-between mb-1" v-for="(competence, index) in character.competences">
            <span class="min-w-[130px]">{{ competence.nom }}</span>
            <span class="box font-bold text-primary">{{ competence.bonus_total }}</span>
            <span> = </span>
            <span class="min-w-[30px]">{{ competence.modif_cara }}</span>
            <span class="box" v-if="character.caracs_modif[competence.modif_cara] != null"> {{ `${character.caracs_modif[competence.modif_cara] > 0 ? "+" : ""}${character.caracs_modif[competence.modif_cara]}` }}</span>
            <span class="box" v-else></span>
            <span> + </span>
            <maitrise :qual="competence.maitrise" :niveau="character.niveau" />
            <span> + </span>
            <span class="box">{{ competence.modif_div }}</span>
        </div>
    </div>
</template>

<script lang="ts" setup>
const props = defineProps(["character"]);
</script>
