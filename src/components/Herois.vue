<template>
    <div class="home">
        <NavBar @enviarId="atualizarId"/>
        <div id="div-pai">

            <div class="conteiner">
                <InfoHeroi :descricao="descricao" :name="name" :url="url"/>
                <div class="coomics-conteiner events">
                    <Events :nameEvents="nameEvents" :thumbnailEvents="thumbnailEvents"/>
                    <button id="btn-events" class="" @click="getEvents()">></button>
                </div>
            </div>

            <div class="coomics-conteiner">
                <div class="coomics-conteiner">
                    <Commics :nameCommic="nameCommics" :thumbnailCommics="thumbnailCommics"/>
                    <button @click="getCommics()">></button>
                </div>
                <img :src="fotoPersonagemAtual"/>
            </div>

        </div>   
    </div>
</template>

<script>

    import NavBar from '../components/NavBar.vue'
    import InfoHeroi from '../components/InfoHeroi.vue'
    import Commics from '../components/Comics.vue'
    import Events  from '../components/Events.vue'

    export default {
        name:"Herois",
        props: ['idHeroiAtual'],
        components: {
            InfoHeroi,
            NavBar,
            Commics,
            Events
        },

        data(){
            return{
                name:"",
                url: "",
                descricao:"",
                timeStamp:'1661625932',
                apiKey: '1579b3df5e35edac1ffffd967ccede4a',
                md5: 'fab757d0d8f575804952174156779009',
                dados: null,
                idHeroi: this.idHeroiAtual,
                UrlCommics: null,
                nameCommics: null,
                thumbnailCommics: null,
                positionCommic: 0,
                totalCommic: [],

                UrlEvents: null,
                nameEvents: null,
                thumbnailEvents: null,
                positionEvents: 0,
                totalEvents: [],

                fotoPersonagemAtual: null
            }
        },

        mounted(){
            this.getHerois(this.idHeroi)
        },  

        methods:{

            atualizarId(id){
                this.idHeroi = id
                this.getHerois(this.idHeroi)
                this.positionCommic = 0
                this.getUrlCommics()
                this.positionEvents = 0
                this.getEvents()
                
                if(id == 1009610){
                    this.fotoPersonagemAtual = '/img/spiderman.4f88f637.png'
                }

                if(id == 1011025){
                    this.fotoPersonagemAtual = '/img/Thor-PNG.cf4214ff.png'
                }

                if(id == 1009718){
                    this.fotoPersonagemAtual = '/img/wolverine_PNG37.09c4057d.png'
                }

                if(id == 1009351){
                    this.fotoPersonagemAtual = '/img/Herói-Hulk-PNG.7491be8b.png'
                }

            },
            
            getHerois(id){

                if(id == 1009610){
                    this.fotoPersonagemAtual = '/img/spiderman.4f88f637.png'
                }

                if(id == 1011025){
                    this.fotoPersonagemAtual = '/img/Thor-PNG.cf4214ff.png'
                }

                if(id == 1009718){
                    this.fotoPersonagemAtual = '/img/wolverine_PNG37.09c4057d.png'
                }

                if(id == 1009351){
                    this.fotoPersonagemAtual = '/img/Herói-Hulk-PNG.7491be8b.png'
                }
            
                fetch("https://gateway.marvel.com:443/v1/public/characters/"+id+"?ts="+this.timeStamp+"&apikey="+this.apiKey+"&hash="+this.md5+"&limit=1"
                ).then((response) => {
                    return response.json();
                }).then((jsonParsed) => {
                    console.log(jsonParsed);
                    const dados = jsonParsed
                    this.descricao = dados.data.results[0].description
                    this.name = dados.data.results[0].name

                    var urlAux = dados.data.results[0].thumbnail.path
                    var extensionAux = dados.data.results[0].thumbnail.extension
                    this.url = urlAux+"."+extensionAux

                    this.UrlCommics = dados.data.results[0].comics.items[this.positionCommic].resourceURI
                    this.nameCommics = dados.data.results[0].comics.items[this.positionCommic].name
                    this.totalCommic = dados.data.results[0].comics.items
                    this.totalCommic = this.totalCommic.length
                    this.getUrlCommics()

                    if (dados.data.results[0].events.items.length == 0 || dados.data.results[0].events.items.length == '0'){
                        this.UrlEvents = dados.data.results[0].series.items[this.positionEvents].resourceURI
                        this.nameEvents = dados.data.results[0].series.items[this.positionEvents].name
                        this.totalEvents = dados.data.results[0].series.items
                    } else {
                        this.UrlEvents = dados.data.results[0].events.items[this.positionEvents].resourceURI
                        this.nameEvents = dados.data.results[0].events.items[this.positionEvents].name
                        this.totalEvents = dados.data.results[0].events.items
                    }
                    
                    this.totalEvents = this.totalEvents.length
                    this.getUrlEvents()

                })
            },

            getCommics(){
                this.positionCommic ++;
                if ((this.totalEvents-1) >= this.positionCommic){
                    this.getHerois(this.idHeroi)
                    this.getUrlCommics();
                } else {
                    this.positionCommic = 0
                    this.getHerois(this.idHeroi)
                }
            },

            getUrlCommics(){
                fetch(this.UrlCommics+"?ts="+this.timeStamp+"&apikey="+this.apiKey+"&hash="+this.md5+"&limit=1"
                ).then((response) => {
                    return response.json();
                }).then((jsonParsed) => {
                    const dados = jsonParsed
                    var urlAux = dados.data.results[0].thumbnail.path
                    var extensionAux = dados.data.results[0].thumbnail.extension
                    this.thumbnailCommics = urlAux+"."+extensionAux
                })
            },

            getEvents(){
                this.positionEvents ++;
                if ((this.totalCommic-1) >= this.positionEvents){
                    this.getHerois(this.idHeroi)
                    this.getUrlEvents();
                } else {
                    this.positionEvents = 0
                    this.getHerois(this.idHeroi)
                }
            },

            getUrlEvents(){
                fetch(this.UrlEvents+"?ts="+this.timeStamp+"&apikey="+this.apiKey+"&hash="+this.md5+"&limit=1"
                ).then((response) => {
                    return response.json(); 
                }).then((jsonParsed) => {
                    const dados = jsonParsed
                    var urlAux = dados.data.results[0].thumbnail.path
                    var extensionAux = dados.data.results[0].thumbnail.extension
                    this.thumbnailEvents = urlAux+"."+extensionAux
                })
            }


        }
        
    }
</script>

<style scoped>

.home{
  display: flex;
  align-items: center;
}

.conteiner{
    display: flex;
    align-items: center;
}

#div-pai{
     display: flex;
     flex-direction: column;
}

.coomics-conteiner{
    display: flex;
    align-items: center;
}

.coomics-conteiner img{
    margin-left: 150px;
    width: 550px;
}

img{
    z-index: 1000;
    margin-bottom: -50px;
}

button{
    width: 40px;
    height: 30px;
    border-radius: 25px;
    border: none;
    margin-top: 100px;
    font-weight: bold;
    background-color: #C72828;
    color: #fff;
}

button:hover{
    cursor:pointer
}

#btn-events{
    margin-top: -15px;
    height: 150px;
    width: 20px;
}

@media screen and (max-width: 1200px) {
    
    .coomics-conteiner img{
       display: none;
    }

    #div-pai{
        display: flex;
        flex-wrap: wrap;
    }

    .events{
        position: absolute;
        margin-top: 380px;
        margin-left: 220px;
    }

    #btn-events{
        margin-top: 380px;
        margin-left: 480px;
        height: 150px;
        width: 20px;
    }

}

@media screen and (max-width: 992px) {
    
    .coomics-conteiner img{
       display: none;
    }

    #div-pai{
        display: flex;
        flex-wrap: wrap;
    }

    .events{
        position: absolute;
        margin-top: 380px;
        margin-left: 220px;
    }

    #btn-events{
        margin-top: 380px;
        margin-left: 480px;
        height: 150px;
        width: 20px;
    }

}

@media screen and  (max-width: 900px) {

    #div-pai{
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .conteiner{
        display: block;
    }

    .events{
        position: absolute;
        margin-top: 200px;
        margin-left: 95px;
    }

    #btn-events{
        margin-bottom: 150px;
        margin-left: 350px;
        height: 150px;
        width: 20px;
    }

}


@media screen and (min-width: 0px) and (max-width: 800px) {

    #div-pai{
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .events{
        display: none;
    }

    #btn-events{
        display: none;
    }

}

</style>