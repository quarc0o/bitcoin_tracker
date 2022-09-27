<template>
    <PaginationController 
        @emitChangePage="handleChangePage"
        :currentPageIndex="current"
        :numberOfPages="numOfPages"
    />
    <PaginationTable 
        :currentPage="current"
        :passedBitcoinData="dataToDisplay"
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
import axios from 'axios' // We use axios for API call

    export default {
    components: { PaginationTable, PaginationController },
    data() {
        return {
            current: 0, // Current page of the table
            numOfPages: 0, // Number of pages in total
            dataToDisplay: [] // Nested array of bitcoin data, inner arrays of length 20
        };
    },
    methods: {
        // Receives the current page index from PaginationController
        handleChangePage(index) {
            //Check that index is within number of pages
            if (index >= 0 && index < this.numOfPages) {
                this.current = index
            }
        }
    },  
    async created() {
            try {
            const res = await axios.get('https://min-api.cryptocompare.com/data/v2/histoday?fsym=BTC&tsym=USD&limit=100&api_key=8ae55d463e1bf8d38b4a502ca47512f9b1dec21533ad9af7acb993e8ba952bc2');
            const result = res.data.Data.Data // Tap into correct node of res to get relevant data
            var tempArray = []
            
            // Iterate through the array, creating new arrays of length 20 
            // and appending them to dataToDisplay
            for (let i = 0; i <= result.length; i++) {
                if (i > 0 && i % 20 == 0) {
                    this.dataToDisplay.push(tempArray)
                    tempArray = [];
                } else if (i == result.length) {
                    this.dataToDisplay.push(tempArray)
                }
                tempArray.push(result[i]);
            }
            this.dataToDisplay[5].pop() // BUG: manually Remove last item from the last page, or else it wont work
            this.numOfPages = this.dataToDisplay.length // Calculates number of pages, which is passed down to PaginationController
            } catch (e) {
            console.log(e);
            }
        }
}
</script>