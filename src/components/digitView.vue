<script setup>
import { computed, ref, onMounted } from 'vue';
import Digit from "./digit.vue";
import DigitRuler from './digitRuler.vue';
const
    props = defineProps({
        num: String,
        start: Number,
    }),
    view = ref(null),
    width = ref(0),
    unit = computed(() => width.value / 32),
    digits = computed(() => {
        if (!props.num) return []
        return props.num
            .split("")
            .reverse()
            .map((d, i) => ([d, i]))
    })

function resize() {
    width.value = view.value?.offsetWidth || 0
}

onMounted(() => {
	resize()
	window.addEventListener(
		'resize',
		resize
	)
})
</script>

<template>
    <div
        digit-view
        :ref="(el) => (view = el)"
        :style="{ '--unit': `${unit}px`}"
    >
        <div digit-view-lo>
            <digit v-for="(el, i) in digits" :key="i" :pos="el[1]">
                {{ el[0] }} 
            </digit>
            <digit-ruler :start=0 />
        </div>
        <div digit-view-hi>
            <digit v-for="(el, i) in digits" :key="i" :pos="el[1]">
                {{ el[0] }} 
            </digit>
            <digit-ruler :start=32 />
        </div>
    </div>
</template>

<style scoped lang="scss">
[digit-view-lo],
[digit-view-hi] {
    position: relative;
	height: calc(2 * var(--unit));
	font-size: calc(0.6 * var(--unit));
    user-select: none;
    -webkit-user-select: none;
    --padding: calc(0.1 * var(--unit));
    --digit-blk-top: calc(0.5 * var(--unit));
    & > * {
		position: absolute;
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, 'Noto Sans', sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji';;
		:deep([content]) {
			position: absolute;
			font-family: monospace, monospace;
			text-align: center;
			top: var(--padding);
			left: var(--padding);
			right: var(--padding);
			bottom: var(--padding);
			border-radius: calc(0.1 * var(--unit));
		}
	}
}
[digit-view] {
    position: relative;
    &, :deep(*) {
		transition: none;
	}
}
</style>