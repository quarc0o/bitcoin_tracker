<template>
    <PaginationController 
        @emitChangePage="handleChangePage"
        :currentPageIndex="current"
        :numberOfPages="numOfPages"
    />
    <PaginationTable 
        :currentPage="current"
        @emitNumOfPAges="handleNumOfPages"
    />
    <PaginationController 
        @emitChangePage="handleChangePage"
        :currentPageIndex="current"
        :numberOfPages="numOfPages"
    />
</template>


<script>
import PaginationTable from './PaginationTable.vue';
import PaginationController from './PaginationController.vue';

    export default {
    data() {
        return {
            current: 0, // Current page of the table
            numOfPages: 0 // Number of pages in total
        };
    },
    methods: {
        // Receives the current page index from PaginationController
        handleChangePage(index) {
            //Check that index is within number of pages
            if (index >= 0 && index < this.numOfPages) {
                this.current = index
            }
        },
        // Receives number of pages from PaginationTable
        handleNumOfPages(num) {
            this.numOfPages = num
            console.log('num of pages ' + num)
        }
    },  
    components: { PaginationTable, PaginationController }
}
</script>