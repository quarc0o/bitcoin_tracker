<template>
    <div class="table-container">
        <table>
            <th>Date</th>
            <th>High</th>
            <th>Low</th>
            <th>Close</th>
            <tr v-for="item in dataToDisplay[currentPage]" :key="item.id">
                <td>{{unixToDate(item.time)}}</td>
                <td>{{item.high}}</td>
                <td>{{item.low}}</td>
                <td>{{item.close}}</td>
            </tr>
        </table>
    </div>
</template>

<script>
    import axios from 'axios' // We use axios for API call
    export default {
        data() {
            return {
                dataToDisplay: [], // Nested array of bitcoin data, inner arrays of length 20
            }
        },
        props: ['currentPage'],
        methods: {
            // Calculates number of pages and emits to its parent - BitcoinData,
            // which uses data to display correct ammount of pag-buttons
            emitNumberOfPages() {
                let numOfPages = this.dataToDisplay.length;
                this.$emit('emitNumOfPAges', numOfPages);
            },
            // Converts unix to readable time
            unixToTime(unix) {
                var date = new Date(unix * 1000);
                var hours = date.getHours();
                var min = '0' + date.getMinutes();
                var sec = '0' + date.getSeconds();

                var formattedTime = hours + ':' + min + ':' + sec;
                return formattedTime
            },
            // Converts unix to readable date
            unixToDate(unix) {
                var months = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
                var date = new Date(unix * 1000);
                var year = date.getFullYear();
                var month = months[date.getMonth()]
                var day = date.getDate();
                var fullDate = day + ' ' + month + ' ' + year;
                return fullDate 
            }
        },  
        async created() {
            try {
            const res = await axios.get('https://min-api.cryptocompare.com/data/v2/histoday?fsym=BTC&tsym=USD&limit=100&api_key=8ae55d463e1bf8d38b4a502ca47512f9b1dec21533ad9af7acb993e8ba952bc2');
            const result = res.data.Data.Data // Tap intp correct node of res to get relevant data
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
            this.dataToDisplay[5].pop()
            console.log(this.dataToDisplay[5])
            this.emitNumberOfPages() // After API call we let the parent - BitcoinData know the number of pages
            } catch (e) {
            console.log(e);
        }
      }
    }
</script>

<style>
    table {
        margin: 0 auto;
        border-collapse: collapse;
        width: 800px;
    }
    th {
        font-size: 28px;
        text-align: left;
        padding-left: 20px;
        color: #607EAA;
    }
    td {
        font-size: 22px;
        color: #607EAA;
        padding: 20px;
    }
    tr {
        text-align: left;
    }
    tr:nth-child(even) {
        background-color: #F9F5EB;
    }
    tr:nth-child(odd) {
        background-color: #EAE3D2;
    }
</style>