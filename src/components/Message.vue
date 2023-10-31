<template>
    <div class="message__container">
        <p>{{ msg }}</p>
    </div>
</template>


<script>
export default {
    name: "Message",
    props: {
        msg: String
    }
}

</script>

<style scoped>

.message__container{
    color: #004085;
    background-color: #cce5ff;
    border: 2px solid #b8daff;
    border-radius: 5px;
    padding: 15px;
    max-width: 300px;
    margin: 30px auto;
}

</style>