<template>
    <div class="main">
        <img :src="url"/>
        <div>
            <h3>{{name}}</h3>
            <p>{{descricao}}</p>
        </div>
    </div>
</template>

<script>
    export default {
        name: "InfoHeroi",
        props: ['descricao', 'name', 'url']
    }
</script>

<style scoped>

.main{
    display: flex;
    background-color: #C72828;
    color: #fff;
    width: 700px;
    border-radius: 25px;
    margin-left: 80px;
    transition: 1.5s;
}

.main h3, .main p{
    margin-left: 10px;
    margin-right: 30px;
    text-align: justify;
}

.main h3{
    text-transform: uppercase;
    font-size: 25px;
}

.main p{
    color:rgb(240, 239, 239);
}

.main:hover{
    transform: scale(1.05);
}

img{
    border-top-left-radius: 25px;
    border-bottom-left-radius: 25px;
    width: 250px;
}

@media screen and (max-width: 1080px) {
    .main{
       margin-bottom: 50px;
    }
    
}

@media screen and (min-width: 900px) and (max-width: 992px) {

    .main{
        width: 600px;
        font-size: 14px;
    }

    .main h3{
        text-transform: uppercase;
        font-size: 20px;
    }   

}

@media screen and (min-width: 780px) and (max-width: 900px) {

    .main{
        width: 550px;
        font-size: 13px;
        margin-left: 30px;
    }

    .main h3{
        text-transform: uppercase;
        font-size: 18px;
    }   

}

@media screen and (min-width: 700px) and (max-width: 779px) {

    .main{
        width: 450px;
        height: 250px;
        font-size: 10px;
        margin-left: 30px;
    }

    .main h3{
        text-transform: uppercase;
        font-size: 18px;
    }   

}

@media screen and (min-width: 0px) and (max-width: 699px) {

.main{
    width: 450px;
    height: 250px;
    font-size: 10px;
    margin-left: 30px;
}

.main h3{
    text-transform: uppercase;
    font-size: 18px;
}   

}

</style>