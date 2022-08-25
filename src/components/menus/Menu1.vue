<script setup lang="ts">
    import { ref } from "vue";
    import TitleComponent from "../TitleComponent.vue";
    import Item from './menu1/Item.vue'

    const menuItems = ref(['About', 'Reel', 'Projects', 'Contact'])
    const activeItemIndex = ref(0)
</script>

<template>
    <section>
        <TitleComponent msg="Menu 1" />

        <ul class="flex justify-center gap-x-8">
            <Item v-for="(item, index) in menuItems"
                  @click="activeItemIndex = index"
                  :item="item"
                  :index="index"
                  :activeItemIndex="activeItemIndex"/>
        </ul>
    </section>
</template>

<style scoped lang="scss">

</style>
