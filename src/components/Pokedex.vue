<template>
    <div>
        <div class="loading"> <img src="./icons/loading.gif" /></div>

        <div class="arrows">
            <img src="./icons/angulo-esquerdo.svg" @click="getPokemon(last_id-1)" id="esquerdo" class="arrow" />
            <img src="./icons/angulo-direito.svg" @click="getPokemon(last_id+1)" id="direito" class="arrow" />
        </div>
        <div class="container">
            <div class="header"><span class="nome">nome</span><span class="tipo">tipo</span></div>
            <img id="img" :src="require(`./pokemons/${last_id}.png`)" alt="loading pokemon..." />
            <div class="status">
                <p class="item-status">Vida <img src="./icons/hp.png" alt="icon" /><span class="vida">Vida</span></p>
                <p class="item-status">Ataque <img src="./icons/atk.png" alt="icon" /><span class="ataque">Ataque</span>
                </p>
                <p class="item-status">Defesa <img src="./icons/def.png" alt="icon" /><span class="defesa">Defesa</span>
                </p>
                <p class="item-status">Super atk <img src="./icons/spa.png" alt="icon" /><span class="sa">Ataque</span>
                </p>
                <p class="item-status">Super def <img src="./icons/spd.png" alt="icon" /><span class="sd">Defesa</span>
                </p>
                <p class="item-status">Velocidade <img src="./icons/spe.png" alt="icon" /><span
                        class="velocidade">Vel</span></p>

            </div>
        </div>
        <div class="footer"></div>
    </div>
</template>


<script>

import $ from 'jquery'
import axios from 'axios'

export default {
    name: "pokedex-main",
    data() {
        return {
            last_id: 0
        }
    },
    methods: {
        getPokemon(id) {
            axios.get(`http://ec2-44-203-132-48.compute-1.amazonaws.com:8082/pokemons/${id}`, { withCredentials: true })
                .then(res => {
                    console.log("res name " + res.data.nome)

                    $(".nome").text(res.data.nome + " #" + res.data.id);
                    $(".tipo").text(res.data.tipo);
                    $(".vida").text(res.data.hp);
                    $(".ataque").text(res.data.atk);
                    $(".defesa").text(res.data.def);
                    $(".sa").text(res.data.spa);
                    $(".sd").text(res.data.spd);
                    $(".velocidade").text(res.data.spe);
                    
                    this.last_id = res.data.id;
                    $(".loading").css("display", "none")
                });
        }
    },
    mounted() {
        this.last_id > 0 ? "" : this.getPokemon(1)
    }
}
</script>

<style>
body {
    font-family: 'Open Sans', sans-serif;
    margin: -10px;
    width: 100vw;
    height: 100vh;
    background-color: gainsboro;
    font-size: 18px;
    overflow: hidden;
}

.container {
    width: 100vw;
    height: 500px;
    background: rgb(255, 69, 0);
    background: linear-gradient(120deg, rgba(220, 220, 220, 1) 47%, rgba(255, 69, 0, 1) 47%);
    margin-top: 5%;
}

.header {
    position: relative;
    top: 15px;
    width: 100vw;
    background: #cfc45cc2;
    text-align: start;
}

.nome {
    padding: 10px;
    padding-left: 40px;
    width: 100vw;
    font-weight: bold;
    float: left;
    background: #cfc45cc2;
}

.tipo {
    padding: 10px;
    position: relative;
    top: -45px;
    font-weight: bold;
    background: rgb(44, 41, 41);
    width: 48vw;
    float: right;
    color: white;
    text-align: center;
    background: linear-gradient(120deg, #cfc45c4b 9%, rgba(44, 41, 41, 1) 5%);
}

.footer {
    width: 100vw;
    height: 30px;
    background-color: black;
}

@media screen and (min-width:500px) and (max-width:768px) {
    .status {
        position: relative;
        left: 10% !important;
        top: 100px !important;
    }

    .arrows {
        position: relative !important;
    }

}

@media screen and (min-width: 769px) {
    .status {
        position: absolute;
        float: right;
        right: 12%;
        top: 150px;
    }

    #img {
        margin: 100px;
    }
}

@media screen and (max-width: 768px) {
    .tipo {
        width: 37.5vw;
    }

    .status {
        position: relative;
        top: 110px !important;
        left: 15px;
    }

    .arrows {
        padding-top: 20px !important;
        position: relative !important;
        margin-left: 30% !important;
    }

    #img {
        margin: 30px;
    }
}

#img {
    width: 300px;
    height: 250px;
}

.arrows {
    position: absolute;
    width: 100vw;
    top: 0.2%;
    z-index: 10;
}

.arrow {
    width: 45px;
    padding: 10px;
    background-color: rgba(245, 245, 245, 0.507);
    border-radius: 25px;
    z-index: 10;
}

.arrow:last-child {
    margin-left: 15%;
}

.arrow:active {
    transform: scale(.4);
}

.arrow:hover {
    border-radius: 40%;
    padding: 5px;
    background-color: rgba(255, 255, 255, 0.192);
}

.item-status img {
    width: 25px;
    position: relative;
    float: right;
    margin-left: 10%;
}

.status p {
    color: white;
    text-align: start;
    padding: 10px;
    padding-left: 30px;
    background-color: rgba(255, 255255, 0.479);
    background: linear-gradient(120deg, rgba(44, 41, 41, 1) 79%, #cfc45c4b 79%);
    border-radius: 25px;
    width: 300px;
}

.velocidade,
.vida,
.ataque,
.defesa,
.sa,
.sd {
    float: right;
    padding-right: 70px;
}

.loading {
    position: absolute;
    display: flex;
    z-index: 10;
    top: 0;
    width: 100vw;
    height: 100vh;
    background-color: rgba(169, 169, 169, 0.438);
}

.loading img {
    width: 100px;
    height: 100px;
    margin: auto auto;
}

.advanced {
    position: absolute;
    padding: 10px;
    border-radius: 10px;
    background-color: white;
    left: 10%;
    top: 10%;
    text-decoration: none;
}

.advanced:hover {
    background-color: yellow;
}
</style>