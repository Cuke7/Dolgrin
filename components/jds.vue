<template>
    <div class="flex flex-col">
        <div class="flex text-[0.5rem]">
            <div>JET DE SAUVEGARDE</div>
            <div class="ml-4">TOTAL</div>
            <div class="ml-12">MAÎTRISE</div>
            <div class="ml-12">MODIF. CARAC</div>
            <div class="ml-5">DIVERS</div>
        </div>
        <div v-for="jds in character.JDS" class="flex items-center mb-1 space-x-2">
            <span class="bg-black w-20 text-center text-white self-center">
                {{ jds.name }}
            </span>
            <span class="box font-bold text-primary">
                {{ jds.bonus_total }}
            </span>
            <span> = </span>
            <maitrise :qual="jds.maitrise" :niveau="character.niveau" />
            <span> + </span>
            <span class="box">
                {{ character.caracs_modif[jds.modif_cara] }}
            </span>
            <span> + </span>
            <span class="box">
                {{ jds.modif_div }}
            </span>
        </div>
    </div>
</template>

<script lang="ts" setup>
const props = defineProps(["character"]);
</script>
