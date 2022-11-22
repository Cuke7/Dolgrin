<template>
    <div class="flex flex-col">
        <div class="relative font-mono">
            <input type="text" class="bg-transparent border-2 border-black rounded-lg text-black p-2" :placeholder="placeholder" v-model="input" @focus="focus = true" @blur="focus = false" ref="inputElement" />
            <div class="bg-white z-50 w-52 absolute rounded-lg flex flex-col max-h-52 overflow-y-auto p-2" v-if="focus && results.length > 0">
                <div @mousedown="select(result)" class="hover:bg-primary hover:bg-opacity-20 cursor-pointer rounded-lg p-2" v-for="result in results">{{ result[props.name as keyof typeof result] }}</div>
            </div>
        </div>
    </div>
</template>

<script lang="ts" setup>
import { search } from "fast-fuzzy";
import { computed, ref, onMounted } from "vue";

const props = defineProps(["placeholder", "data", "name", "modelValue"]);
const emit = defineEmits(["update:modelValue"]);

const input = ref("");
const focus = ref(false);
const inputElement = ref<null | HTMLInputElement>(null);

const select = (item: any) => {
    input.value = item.name;
    emit("update:modelValue", item);
};

const results = computed(() => {
    if (input.value.length > 0) {
        return search(input.value, props.data, { keySelector: (obj) => obj[props.name as keyof typeof obj], returnMatchData: true })
            .filter((item) => item.score > 0.8)
            .map((item) => item.item);
    }
    return props.data;
});
</script>
