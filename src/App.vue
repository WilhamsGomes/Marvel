<template>
  <router-view/>
</template>

<style>

@import url('https://fonts.googleapis.com/css2?family=Open+Sans&display=swap');

body{
    margin: 0;
    padding: 0;
    font-family: 'Open Sans';
    background-color: #F8FAFE;
    overflow: hidden;
}

@media screen and (max-width: 1080px) {
    body{
      overflow-y:auto;
      overflow-x: hidden;
    }
}


</style>
