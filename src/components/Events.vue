<template>
    <div class="events">
        <img :src="thumbnailEvents" :alt="thumbnailEvents"/>
         <div id="title">
            <h3>{{nameEvents}}</h3>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Events",
        props: ['nameEvents', 'thumbnailEvents']
    }
</script>

<style scoped>

.events{
    margin-left: 50px;
    width: 250px;
    height: 230px;
    margin-left: 80px; 
    color: #fff;
    margin-top: -12px;
}

.events h3{
    text-align: center;
    font-size: 13px;
    padding: 0px 10px 0px 10px;
}

#title{
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 50;
    background-color: #C72828;
    border-radius: 15px;
    height: 40px;
    width: 230px;
    text-align: center;
    margin-top: -20px;
}

img{
    z-index: 49;
    width: 230px;
    height: 230px;
    border-top-left-radius: 25px;
    border-top-right-radius: 25px;
    transition: 1.5s;
    background-size: cover;
}

</style>