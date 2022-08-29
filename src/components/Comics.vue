<template>
    <div class="comics">
        <div id="title">
            <h3>{{nameCommic}}</h3>
        </div>
        <img :src="thumbnailCommics" :alt="thumbnailCommics"/>
    </div>
</template>

<script>
    export default {
        name: "Commics",
        props: ['nameCommic', 'thumbnailCommics']
    }

</script>

<style scoped>

.comics{
    margin-left: 50px;
    width: 250px;
    height: 400px;
    margin-top: 50px;
    margin-left: 80px;
    color: #fff;
}

.comics h3{
    text-align: center;
    font-size: 13px;
    padding: 0px 10px 0px 10px;
}

#title{
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 50;
    background-color: #C72828;
    border-radius: 15px;
    height: 40px;
    width: 230px;
    margin-bottom: 5px;
    text-align: center;
}

img{
    z-index: 49;
    width: 230px;
    border-radius: 25px;
    transition: 1.5s;
}

img:hover{
    transform: scale(1.02); 
}

</style>