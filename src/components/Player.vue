<script setup>
import {trackList} from './tracks';
import {ref} from 'vue'

// const classPlay = ref("fa fa-play");
const audio = new Audio(trackList[0].src);
// Трек проигрывается
const isPlay = ref(!audio.paused);
// Отображение названия трека и исполнителя
const currentTrack = ref(trackList[0].title)
const currentArtist = ref(trackList[0].artists)
const curentTrackIndex = ref(0);
const cover = ref("http://ecx.images-amazon.com/images/I/51XSHShbPiL.jpg")

function showNameTrack() {
    //change displaying name of track and artist
    currentTrack.value = trackList[curentTrackIndex.value].title;
    currentArtist.value = trackList[curentTrackIndex.value].artists;
    cover.value = trackList[curentTrackIndex.value].preview;
}
function onPlay(event) {
    // меняем иконку
    isPlay.value = !isPlay.value;
    // if (event) {
    //     // console.log(event.target.classList.value);
    // } 

    // playing track
    isPlay.value ? audio.play() : audio.pause();
}

function onBack() {
    //change to curent track
    curentTrackIndex.value = curentTrackIndex.value == 0 ? trackList.length - 1 : curentTrackIndex.value - 1;
    audio.src = trackList[curentTrackIndex.value].src;
    //change displaying name of track and artist
    showNameTrack();
    isPlay.value && audio.play();
}
function onNext() {
    //change to curent track
    curentTrackIndex.value =
      curentTrackIndex.value == trackList.length - 1 ? 0 : curentTrackIndex.value + 1;
    audio.src = trackList[curentTrackIndex.value].src;
    //change displaying name of track and artist
    showNameTrack();
    isPlay.value && audio.play();
}

function changePosition(event) {
    console.log(setPosition(event));
}
function setPosition(event) {
    console.log(event.x, event.y);
}

</script>

<template>
    <div class="wrapper">
    <div class="player__container">
        <div class="player__body">
        <div class="body__cover">
            <ul class="list list--cover">
            <li>
                <a class="list__link" href=""><i class="fa fa-bars"></i></a>
            </li>

            <li>
                <a class="list__link" href=""></a>
            </li>

            <li>
                <a class="list__link" href=""><i class="fa fa-search"></i></a>
            </li>
            </ul>

            <img :src="cover" alt="Album cover" />
            
            <div class="range" @input="setPosition"  @click="changePosition"></div>
        </div>
        
        <div class="body__info">
            <div class="info__album">The Hunting Party</div>

            <div class="info__song" >{{ currentTrack }}</div>

            <div class="info__artist">{{ currentArtist }}</div>
        </div>

        <div class="body__buttons">
            <ul class="list list--buttons">
            <li>
                <a href="#" class="list__link" >
                    <i class="fa fa-step-backward" @click="onBack" ></i>
                </a>
            </li>

            <!-- <li><a href="#" class="list__link" @click="onPlay"><i :class="classPlay" ></i></a></li> -->
            <li><a href="#" class="list__link" @click="onPlay"><i :class="`${isPlay ? 'fa fa-pause' : 'fa fa-play'}`" ></i></a></li>

            <li><a href="#" class="list__link" @click="onNext"><i class="fa fa-step-forward"></i></a></li>
            </ul>
        </div>
        </div>

        <div class="player__footer">
        <ul class="list list--footer">
            <li><a href="#" class="list__link"><i class="far fa-heart"></i></a></li>
            
            <li><a href="#" class="list__link"><i class="fa fa-random"></i></a></li>
            
            <li><a href="#" class="list__link"><i class="fa fa-undo"></i></a></li>
            
            <li><a href="#" class="list__link"><i class="fa fa-ellipsis-h"></i></a></li>
        </ul>
        </div>
    </div>
    </div>
</template>

<style scoped>
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css";
/* https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.6.3/css/font-awesome.min.css */
/* https://fonts.googleapis.com/css?family=Roboto:300,400,500,700 */
@import '../css/style.css';
</style>
