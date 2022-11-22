<template>
    <div class="flex flex-col justify-between">
        <div class="flex text-[0.5rem]">
            <div>CARAC</div>
            <div class="ml-8">VALEUR</div>
            <div class="ml-7">MODIF</div>
        </div>
        <div v-for="carac in Object.keys(character.caracs)" class="flex flex-col justify-between">
            <div class="flex items-center space-x-4">
                <span class="bg-black text-white w-11 text-center py-1">
                    {{ carac }}
                </span>
                <span class="box">
                    {{ character.caracs[carac] }}
                </span>
                <span class="box font-bold text-primary" v-if="character.caracs_modif[carac] != null"> {{ `${character.caracs_modif[carac] > 0 ? "+" : ""}${character.caracs_modif[carac]}` }} </span>
                <span class="box" v-else> </span>
            </div>
        </div>
    </div>
</template>

<script lang="ts" setup>
const props = defineProps(["character"]);
</script>
