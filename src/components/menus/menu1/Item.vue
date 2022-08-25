<script setup lang="ts">
import { onMounted, ref } from "vue";

    defineProps<{
        item: string,
        index: number,
        activeItemIndex: number
    }>()

    const firstSpan =ref()
    const secondSpan =ref()
    const firstSpanActive = ref(false)
    const secondSpanActive = ref(false)
    const isTransitioning = ref(false)
    const isMouseHover = ref(false)

    const mouseIn = () => {
        isMouseHover.value = true
        if (!isTransitioning.value) firstSpanActive.value = secondSpanActive.value = isTransitioning.value = true
    }

    const mouseOut = () => {
        isMouseHover.value = false
        if (!isTransitioning.value && firstSpanActive.value && secondSpanActive.value) {
            firstSpanActive.value = secondSpanActive.value = false
            isTransitioning.value = true
        }
    }

    const transitionEndListener = (elmt: any, variable: any) => {
        elmt.value.addEventListener('transitionend', () => {
            isTransitioning.value = false
            if (!isMouseHover.value) variable.value = false
        })
    }

    onMounted(() => {
        transitionEndListener(firstSpan, firstSpanActive)
        transitionEndListener(secondSpan, secondSpanActive)
    })
</script>

<template>
    <li class="uppercase">
        <a href="#" class="flex flex-col relative Underline"
           :class="index === activeItemIndex ? 'isActive' : ''"
           @mouseenter="mouseIn"
           @mouseleave="mouseOut">
            <span class="absolute transition duration-450 transform -translate-y-full opacity-0"
                  ref="firstSpan"
                  :class="[firstSpanActive ? 'firstSpanActive' : '', index !== activeItemIndex ? 'notActive' : '']">{{ item }}</span>
            <span class="transition duration-450 transform"
                  ref="secondSpan"
                  :class="[secondSpanActive ? 'secondSpanActive' : '', index !== activeItemIndex ? 'notActive' : '']">{{ item }}</span>
        </a>
    </li>
</template>

<style scoped lang="scss">
.firstSpanActive.notActive {
    @apply translate-y-0 opacity-100;
}

.secondSpanActive.notActive {
    @apply translate-y-full opacity-0;
}

.Underline {
    @apply relative;

    &::after {
        content: '';
        @apply block absolute bottom-0 w-full h-0.5 bg-[#213547] transition-transform transform duration-250 scale-0 origin-left ease-in-out;
    }

    &.isActive::after {
        @apply scale-100;
    }
}
</style>
