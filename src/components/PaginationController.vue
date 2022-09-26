<template>
    <div class="pag-buttons">
        
        <!--First page button-->
        <PaginationButton 
            buttonLabel="<<"
            @click="$emit('emitChangePage', 0)"
        />

        <!--Previous page button-->
        <PaginationButton 
            buttonLabel="<"
            @click="$emit('emitChangePage', currentPageIndex - 1)"
        />

        <!--Numbered buttons-->
        <PaginationButton 
            v-for="(item, index) in new Array(numberOfPages)"
            :key="item"
            :buttonLabel="index+1"
            :isActive="index == currentPageIndex"
            @click="$emit('emitChangePage', index)"
        />

        <!--Next page button-->
        <PaginationButton 
            buttonLabel=">"
            @click="$emit('emitChangePage', currentPageIndex + 1)"
        />

        <!--Last page button-->
        <PaginationButton 
            buttonLabel=">>"
            @click="$emit('emitChangePage', numberOfPages - 1)"
        />
    </div>
</template>

<script>
import PaginationButton from './PaginationButton.vue';
    export default {
    data() {
        return {
        };
    },
    components: { PaginationButton },
    props: {
        currentPageIndex: Number,
        numberOfPages: Number
    }
}
</script>

<style>
    .pag-buttons {
        display: flex;
        justify-content: center;
        gap: 10px;
        padding: 20px 0;
    }
</style>