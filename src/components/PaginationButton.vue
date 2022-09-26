<template>
    <button :class="{ activeBtn: isActive}">{{buttonLabel}}</button>
</template>

<script>
    export default {
        data() {
        },
        props: {
            buttonLabel: String,
            isActive: Boolean
        }
    }
</script>
<style>
button {
    color: #607EAA;
    font-size: 25px;
    padding: 5px 10px;
    background: transparent;
    border: none;
    cursor: pointer;
    border-radius: 5px;
}

.activeBtn {
    color: #F9F5EB;
    background-color: #1C3879;
    box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
}
</style>