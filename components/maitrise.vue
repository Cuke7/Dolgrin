<template>
    <div class="flex space-x-1">
        <div v-for="niv in niveaux" class="flex flex-col mt-auto">
            <div class="text-[0.5rem]">{{ niv }}</div>
            <div v-if="qual != niv" class="h-2 w-2 border-2 border-black" />
            <div v-else class="h-2 w-2 bg-black" />
        </div>
        <div class="box">{{ getBonus() }}</div>
    </div>
</template>

<script setup lang="ts">
const props = defineProps(["qual", "niveau"]);
const niveaux = ["Q", "E", "M", "L"];

const getBonus = () => {
    switch (props.qual) {
        case null:
            return null;
        case "I":
            return 0;
        case "Q":
            return 2 + props.niveau;
        case "E":
            return 4 + props.niveau;
        case "M":
            return 6 + props.niveau;
        case "L":
            return 8 + props.niveau;
    }
};
</script>
