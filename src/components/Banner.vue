<template>
    <div id="main__banner">
        <h1 class="main__banner__text">Faça seu Hamburguer</h1>

    </div>
</template>

<script>
export default {
    name: "Banner"
}
</script>

<style lang="css">

#main__banner{
    width: 100%;
    height: 500px;
    background-image: url('/public/img/burger.jpg') ;
    background-position: 0 -250px;
    background-size: cover;
    background-repeat: no-repeat;
    display: flex;
    align-items: center;
    justify-content: flex-start;

}

.main__banner__text{
    color: #ffff;
    text-align: center;
    background-color: #222;
    font-size: 60px;
    padding: 20px 40px;
    transition: all 0.5s;
}

@media (max-width: 950px) {
    .main__banner__text{
        font-size: 50px;
    }
}
</style>