<script setup lang="ts">
    import { onMounted, ref } from "vue";
    import TitleComponent from "../TitleComponent.vue";
    import boylan1 from '../../../src/assets/slider1/boylan1.png'
    import boylan2 from '../../../src/assets/slider1/boylan2.png'
    import boylan3 from '../../../src/assets/slider1/boylan3.png'
    import boylan4 from '../../../src/assets/slider1/boylan4.png'

    import emblaCarouselVue from 'embla-carousel-vue'
    import ClassNames from 'embla-carousel-class-names'


    const products = ref([
        {
            image: boylan1,
            title: "Boylan - Black Cherry",
            promoMsg: "Nouvelle recette !"
        },
        {
            image: boylan2,
            title: "Boylan - Creme",
        },
        {
            image: boylan3,
            title: "Boylan - Ginger Ale",
            promoMsg: "New"
        },
        {
            image: boylan4,
            title: "Boylan - Shirley Temple",
        }
        ])

    const options = { selected: 'isActive' } // Options

    const [emblaNode] = emblaCarouselVue({
        loop: false,
    }, [ClassNames(options)])
</script>

<template>
    <section>
        <TitleComponent msg="Slider 1" />

        <div class="container mx-auto">
            <div class="embla" ref="emblaNode">
                <div class="embla__container">
                    <div class="embla__slide" v-for="product in products">
                        <div class="bg-yellow-50 rounded-xl border-3 border-black py-8">
                            <img :src="product.image" alt="" class="h-full mx-auto">
                            <h3 class="mt-4 text-3xl">{{ product.title }}</h3>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<style scoped lang="scss">
.embla {
    overflow: hidden;
}
.embla__container {
    display: flex;
}
.embla__slide {
    flex: 0 0 50%;
    @apply px-8;

    &:nth-of-type(1) {
        h3 {
            @apply font-DynaPuff font-bold;
        }
    }

    &:nth-of-type(2) {
        h3 {
            @apply font-PassionOne font-black uppercase;
        }
    }
}
</style>
