<template>

  <div class="container-fluid bg-black vh-100 w-100 p-0">

    <div class="top-app row bg-success m-0" style="height: 90%; border-bottom-left-radius: 48px; border-bottom-right-radius: 48px;">
      <div class="top-app-left col-2 bg-grey-dark" style="border-bottom-left-radius: 48px;">

        <div class="mt-3">
          <h4 class="text-white mb-4">MENU</h4>
          <div class="d-flex align-items-center mb-5" role="button" v-for="(menu ,index) in menus" :key="index" @click="menuAction(menu.alt)">
            <img width="40" class="pe-3" v-bind:src="require(`../assets/icon/${menu.nameImage}`)" alt="image maison" >
            <p class="m-0 fw-bold text-white">{{ menu.alt }}</p>
          </div>
        </div>

      </div>
      <div class="top-app-right col-10 bg-white overflow-hidden" style="border-bottom-right-radius: 48px;">
        <div class="w-100 d-flex justify-content-center align-items-center " style="height: 10%;">
          <div class="row bg-black w-75 p-1" style="border-radius: 20px; height: 50%">
            <input class="col-11 h-100 bg-transparent" type="search" name="" id="" style="width: 95%" placeholder="Rechercher un son ou un artiste">
            <div class="col-1 h-100 d-flex align-items-center justify-content-center" style="width: 5%">
              <img v-bind:src="require('@/assets/icon/Search.png')" alt="Search icon" width="25">
            </div>
          </div>
        </div>
        <div class="w-100 d-flex justify-content-center " style="height: 40%; padding-left:3%; padding-right: 3%">
          <div class="bg-grey-light w-100 d-flex flex-column justify-content-between" style="border-radius: 20px;">
            <h1 class="text-white fw-bold " style="font-size:xxx-large;text-align: center" >TITRE SON</h1>
            <div class="ps-2" style="height:15%">
              <img class="img-fluid h-100 p-1" :src="require('@/assets/icon/ic_play_circle_outline_48px.png')" alt="icon play">
            </div>
          </div>
        </div>
        <div class="w-100 pt-3 fw-bold " style="height: 50%; padding-left:3%; padding-right: 3%">
          <p>Liste De Lecture</p>

          <!---------------------------- D.E.E ----------------------------->
          <div class="listSong w-100 h-100  overflow-x-scroll "></div>
        </div>
      </div>
    </div>

    <div class="bottom-app container-fluid p-0 bg-black d-flex" style="height: 10%">
      <div class="d-flex align-items-center h-100 ps-4 " style="width: 20%;">
        <div class="rounded-circle bg-rose" style="width: 20%; height: 75%;border: 4px solid #454545"></div>
        <div class="ps-2">
          <p class="text-white">Mind-Blowing</p>
          <p style="color: #888888; font-size: x-small;">various Artiste</p>
        </div>
      </div>
      <div class="d-flex align-items-center justify-content-between" style="width: 60%;">
        <div class="h-50 d-flex justify-content-between align-items-center" style="width: 40%;">
          <img class="img-fluid h-50 " :src="require('@/assets/icon/button-shuffle.png')" alt="icon play">
          <img class="img-fluid h-50" :src="require('@/assets/icon/back.png')" alt="icon play">
          <div class="rounded-circle bg-white h-100  d-flex align-items-center justify-content-center playsSong" style="width: 10%;">
            <img class="img-fluid h-50" :src="require('@/assets/icon/plays.png')" alt="icon play">
          </div>
          <img class="img-fluid h-50" :src="require('@/assets/icon/next.png')" alt="icon play">
          <img class="img-fluid h-50" :src="require('@/assets/icon/ic_repeat_24px.png')" alt="icon play">
        </div>
        <div class="h-50 d-flex align-items-center" style="width: 58%;">
          <p class="text-white me-1">00:00:00</p>
          <input class="progress-son" type="range" min="1" max="100" value="0" >
          <p class="text-white ms-1">00:00:00</p>
        </div>
      </div>
      <div class="d-flex align-items-center" style="width: 20%;">
        <div class="h-50 w-100 d-flex p-1 align-items-center">
          <img class="img-fluid h-50 ms-3" :src="require('@/assets/icon/playlist-fill.png')" alt="icon play">
          <img class="img-fluid h-50 ms-3" :src="require('@/assets/icon/cast-view.png')" alt="icon play">
          <img class="img-fluid h-50 ms-3" :src="require('@/assets/icon/volume-high-2.png')" alt="icon play">
          <input class="progress-son ms-2 me-3 bg-white" type="range" min="1" max="100" value="0" >
        </div>
      </div>
    </div>

  </div>

</template>

<script setup>
import {onMounted} from 'vue';
import dataSong from '@/assets/data/song.json'

let songEnCourDeLecture = new Audio();

//apres avoir monter tout les elements html
onMounted(()=> {

  const playsSong = document.querySelector(".playsSong");
  const divListSong = document.querySelector(".listSong");

  for (let i in dataSong) {

    let audio = new Audio(require('@/assets/song/' + dataSong[i].music));

    audio.addEventListener('loadedmetadata', function() {

      let duree = audio.duration;

      let hours = Math.floor(duree / 3600);
      let minutes = Math.floor((duree % 3600) / 60);
      let seconds = Math.floor(duree % 60);

      let durrerTotale = `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;

      const divConteneurItemeSong = document.createElement("div");

      divConteneurItemeSong.classList.add("w-50");
      divConteneurItemeSong.classList.add("d-flex");
      divConteneurItemeSong.classList.add("justify-content-between");
      divConteneurItemeSong.classList.add("align-items-center");
      divConteneurItemeSong.classList.add("mt-3");

      divConteneurItemeSong.style.height= "15%";
      divConteneurItemeSong.innerHTML = `

     <div class="d-flex align-items-center h-100" >
               <div class="h-100 rounded bg-grey-light" style="width:50px;"></div>
                 <p class="ms-2" >${ dataSong[i].artist }</p>
              </div>
              <p>Genre du song</p>
              <p> ${ durrerTotale }</p>

              <div class="d-flex align-items-center justify-content-between h-75" style="width: 20%;">
                <img  class="img-fluid h-50" src=" ${ require('@/assets/icon/heart.png') }" alt="icon play" srcset="">
                <img  class="img-fluid h-50"  src=" ${ require('@/assets/icon/trash.png') } " alt="icon play" srcset="">
                <img class="img-fluid" style="width: 20%;" src=" ${ require('@/assets/icon/Dots.png') } " alt="icon play" srcset="">
              </div>
     </div>
     `;

      divListSong.appendChild(divConteneurItemeSong);
    });
  }

  playsSong.addEventListener("click", () => {
    jouer()
  });

});

const menus = [
  { nameImage: "home-water.png", alt: "Dossier" },
  { nameImage: "music-cascade.png", alt: "Songs" },
  { nameImage: "playlist.png", alt: "Playlist" },
  { nameImage: "user-list.png", alt: "Just for You" }
]

function menuAction(nameMenu) {

  switch (nameMenu) {
    case "Dossier":console.log(`L'utilisateur a cliqué sur l'image ${1}`); break;
    case "Songs":console.log(`L'utilisateur a cliqué sur l'image ${2}`);break;
    case "Playlist":break;
    case "Just for You":break;
  }
}

chargerSong(0)

function chargerSong(index) {
  songEnCourDeLecture.src = require('@/assets/song/' + dataSong[index].music)
  songEnCourDeLecture.load()
}

function jouer() {
    songEnCourDeLecture.play()
}

</script>

<style scoped>

input[type="search"]{
  outline: none;
  border: none;
  padding-left: 1%;
  color: white;
}

input[type="search"]::placeholder{
  color: white;
  opacity: 1; /* Firefox */
}

.progress-son{
  width: 100%;
  border-radius: 20px;
  appearance: none;
  height: 4px;
  background-color: #9c1855;
  transition: opacity 0.2s;
}

.progress-son::-webkit-slider-thumb{
  -webkit-appearance: none;
  height: 15px;
  width: 15px;
  background: #9c1855;
  border-radius: 50%;
  border: 3px solid white;
  cursor: pointer;
}

</style>