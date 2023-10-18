<template>

  <div class="container-fluid bg-black vh-100 w-100 p-0">

    <div class="top-app row bg-success m-0" style="height: 90%; border-bottom-left-radius: 48px; border-bottom-right-radius: 48px;">
      <div class="top-app-left col-2 bg-grey-dark" style="border-bottom-left-radius: 48px;">

        <div class="mt-3">
          <h4 class="text-white mb-4">MENU</h4>
          <div class="d-flex align-items-center mb-5" v-for="menu in menus" :key="menu.nameImage">
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
        <div class="w-100 pt-3 fw-bold" style="height: 50%; padding-left:3%; padding-right: 3%">
          <p>Liste De Lecture</p>
        </div>
      </div>
    </div>

    <div class="bottom-app container-fluid bg-black" style="height: 10%">
    </div>

  </div>

</template>

<script setup>

const menus = [
  { nameImage: "home-water.png", alt: "Home" },
  { nameImage: "music-cascade.png", alt: "Songs" },
  { nameImage: "playlist.png", alt: "Playlist" },
  { nameImage: "user-list.png", alt: "Just for You" },
]

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

</style>