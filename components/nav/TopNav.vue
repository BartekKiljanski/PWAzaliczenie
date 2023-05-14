<template>
<div class="nav">

    <div class="item"><span>1</span>1</div>
    <div class="item"><span>2</span>2</div>
</div>

</template>
<script></script>

<style scoped>
.nav {
    display: flex;
    border: 3px solid red;
    height: 100%;
    width: 100%;
    max-height: 200px;
    min-height: 200px;
    max-width: 1000px;
    min-width: 200px
}
.item {
border: 3px solid red;
width: 20px;
height: 39px;
}
.item2 {
    display: flex;
    border: 3px solid blue;
width: 20px;
height: 39px;
    flex-direction: column;
}
</style>