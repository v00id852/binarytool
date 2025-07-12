<script setup>
import { computed } from 'vue'
const props = defineProps({
    start: Number
})
const list = computed(() => Array.from({ length: 32 }, (_, i) => props.start + i))
</script>

<template>
    <div style="
			position: absolute;
			top: 0;
			left: 0;
			right: 0;
			bottom: 0;
			opacity: 0.5;
		">
        <div v-for="pos in list" :key="pos % 32" :style="{ '--pos': pos % 32 }">
            <div
                rule-text
                class='center'
            >
                {{ pos }}
            </div>
        </div> 
    </div>
</template>

<style scoped lang="scss">
[rule-text] {
	position: absolute;
	--x: calc(var(--pos) * var(--unit));
	--c: var(--ct-gray-dark);
	top: 0;
	color: var(--c);
	font-size: 0.7em;
	font-weight: bold;
	line-height: 100%;
	&.center {
		right: var(--x);
		width: var(--unit);
		text-align: center;
	}
}
</style>