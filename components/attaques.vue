<template>
    <div class="flex flex-col space-y-1">
        <div v-for="attaque in character.attaques" class="flex flex-col">
            <div class="flex text-[0.5rem] ml-52">
                <span class="ml-6">TOTAL</span>
                <span class="ml-9">CAR.</span>
                <span class="ml-14">MAÎTRISE</span>
                <span class="ml-[65px]">DIV</span>
            </div>
            <div class="flex space-x-2">
                <span class="bg-black text-center text-white w-[220px] h-[1.5rem]">{{ attaque.nom }}</span>
                <span class="box font-bold text-primary text-center">{{ attaque.bonus_total }}</span>
                <span> = </span>
                <span class="box">
                    {{ character.caracs_modif[attaque.modif_cara] }}
                </span>
                <span> + </span>
                <maitrise :qual="attaque.maitrise" :niveau="character.niveau" />
                <span> + </span>
                <span class="box ml-4">{{ attaque.modif_div }}</span>
            </div>
            <div class="flex flex-col mr-auto mt-1">
                <div class="text-[0.5rem]">
                    <span> DÉGÂTS </span>
                    <span class="ml-20"> TRAITS </span>
                </div>
                <div class="flex">
                    <span class="px-2 w-20 h-[1.5rem] border-2 border-black flex items-center justify-center">
                        {{ attaque.des_degats }}
                    </span>
                    <span class="box rounded-xl px-2 mx-4" v-for="trait in attaque.traits">
                        {{ trait }}
                    </span>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts" setup>
const props = defineProps(["character"]);
</script>
