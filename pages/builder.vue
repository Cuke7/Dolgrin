<template>
    <div class="h-full flex pageBg justify-center items-center flex-col w-full">
        <div class="flex space-x-4">
            <picker placeholder="Pick a class" :data="allClasses" name="name" v-model="classe" />
            <picker placeholder="Pick an ancestry" :data="allAncestries" name="name" v-model="ancestry" />
        </div>
        <div v-for="level in 5" class="flex flex-col my-4" v-if="classe && ancestry">
            <div class="text-primary text-xl">Level {{ level }}</div>
            <div v-if="classe.data.ancestryFeatLevels.value.includes(level)">
                <picker placeholder="Ancestry feat"></picker>
            </div>
            <div v-if="classe.data.classFeatLevels.value.includes(level)">
                <picker placeholder="Class feat"></picker>
            </div>
        </div>
    </div>
</template>

<script lang="ts" setup>
import { onMounted, ref } from "vue";

const allClasses = ref<any>();
const allAncestries = ref<any>();
const classe = ref();
const ancestry = ref();

onMounted(async () => {
    const data = await $fetch(`/api/getDataSet?dataSetName=classes`);
    console.log(data.ranger);
    allClasses.value = Object.values(data);
    allAncestries.value = Object.values(await $fetch(`/api/getDataSet?dataSetName=ancestries`));
    classe.value = allClasses.value[0];
    ancestry.value = allAncestries.value[0];
});
</script>

<style scoped>
.pageBg {
    background-image: url("./background.jpg");
    background-repeat: repeat;
}
</style>
