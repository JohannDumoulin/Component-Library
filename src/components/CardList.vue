<script setup lang="ts">
import TitleComponent from "./TitleComponent.vue";
import CardItem from "./cardList/CardItem.vue";
</script>

<template>
    <section>
        <TitleComponent msg="Card List" />

        <div class="container mx-auto">
            <div class="flex flex-wrap -m-4">
                <CardItem v-for="card in 7"/>
            </div>
        </div>

    </section>
</template>

<style scoped>

</style>
