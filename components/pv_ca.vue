<template>
    <div class="flex flex-col">
        <div class="flex mb-2 items-center">
            <div class="px-2 text-center bg-black text-white mr-2 py-1">PV max</div>
            <div class="text-primary font-bold mr-8">
                {{ character.PV == 0 ? " " : character.PV }}
            </div>
            <div class="px-2 ml-10 text-center bg-black text-white py-1">PV actuel</div>
        </div>
        <!-- CA -->
        <div class="flex text-[0.5rem] ml-20">
            <span class="ml-5">DEX</span>
            <span class="ml-9">ARMURE</span>
            <span class="ml-11">MAÎTRISE</span>
            <span class="ml-11">DIVERS</span>
        </div>
        <div class="flex items-center space-x-1">
            <span class="box font-bold text-primary">
                {{ character.CA.bonus_total }}
            </span>
            <span>= 10 +</span>
            <span class="box">
                {{ character.armure.DEX_max }}
            </span>
            <span> + </span>
            <span class="box">
                {{ character.armure.bonus_CA }}
            </span>
            <span> + </span>
            <maitrise :qual="character.armure.maitrise" :niveau="character.niveau" />
            <span> + </span>
            <span class="box">{{ character.armure.modif_div }}</span>
        </div>
        <div class="flex flex-col">
            <div class="flex text-[0.5rem]">
                <span class="">ARMURE</span>
                <span class="ml-40 pl-2">BONUS CA</span>
                <span class="ml-4">DEX MAX</span>
            </div>
            <div class="flex space-x-4">
                <span class="px-2 bg-black text-center text-white self-center w-1/2 h-[1.5rem]">{{ character.armure.name }} </span>
                <span class="box"> {{ character.armure.bonus_CA }}</span>
                <span class="box"> {{ character.armure.DEX_max }}</span>
            </div>
        </div>
    </div>
</template>

<script lang="ts" setup>
const props = defineProps(["character"]);
</script>
