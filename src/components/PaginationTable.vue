<template>
    <div class="table-container">
        <table>
            <th>Date</th>
            <th>High</th>
            <th>Low</th>
            <th>Close</th>
            <tr v-for="item in passedBitcoinData[currentPage]" :key="item.id">
                <td>{{unixToDate(item.time)}}</td>
                <td>{{item.high}}</td>
                <td>{{item.low}}</td>
                <td>{{item.close}}</td>
            </tr>
        </table>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                
            }
        },
        props: {
            currentPage: Number,
            passedBitcoinData: []
        },
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