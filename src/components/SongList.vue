<template>
    <div v-if="!isPlayerVisible">
        <div class="text-blue-300 font-bold text-center text-3xl mb-8 mt-4">
            VueJS SingFy
        </div>
        <div 
            v-for="(song, songIndex) in list" v-bind:key="song.id"
            class="flex flex-row justify-between mb-4 cursor-pointer"
            v-on:click="playSong(songIndex)"
        >
            <div>
                <span class="text-blue-400">{{ song.name }}</span>
                <br/>
                <span class="text-yellow-400">{{ song.artistName }} - {{ song.albumName }}</span>
            </div>
            <div>
                <img 
                    class="max-h-12 rounded"
                    v-bind:src="song.src" 
                />
                <br/>
            </div>
        </div>
    </div>
    <div v-if="isPlayerVisible">
         <SongPlayer 
            v-bind:song="list[currentSongIndex]"
            @goback="isPlayerVisible = !isPlayerVisible"
            @next="playNext"
            @previous="playPrevious"
         />
    </div>
</template>

<script>
import SongPlayer from './SongPlayer.vue';

export default {
    data () {
        return {
            isPlayerVisible: true,
            currentSongIndex: 0,
            list: [
                {
                 id: 1,
                    name: 'Cancion 1',
                    artistName: 'Adam Lambert',
                    albumName: 'Everything',
                    year: 2021,
                    src: `https://source.unsplash.com/random/400x400?date=1`,
                    //songSrc: `https://file-examples-com.github.io/uploads/2017/11/file_example_MP3_700KB.mp3`
                    songSrc: `https://filesamples.com/samples/audio/mp3/sample3.mp3`
               },
                {
                    id: 2,
                    name: 'Cancion 2',
                    artistName: 'Roberto IP',
                    albumName: 'Invented Album',
                    year: 1999,
                    src: `https://source.unsplash.com/random/400x400?date=2`,
                    songSrc: `https://filesamples.com/samples/audio/mp3/sample2.mp3`
                },
                {
                    id: 3,
                    name: 'Cancion 3',
                    artistName: 'Adam Hart',
                    albumName: 'Spice It Up',
                    year: 2013,
                    src: `https://source.unsplash.com/random/400x400?date=3`,
                    songSrc: `https://filesamples.com/samples/audio/mp3/sample1.mp3`
                }
            ]
        }
    },
    methods: {
        playSong (index){
            this.currentSongIndex = index;
            this.isPlayerVisible = true;
        },
        playNext (){
            if(this.currentSongIndex < this.list.length -1){
                this.currentSongIndex += 1;
            } else{
            this.currentSongIndex = 0;
            }
        },
        playPrevious (){
            if (this.currentSongIndex != 0){
                 this.currentSongIndex -= 1;
            } else {
                this.currentSongIndex = this.list.length -1;
            }
        }
    },
    components:{
        SongPlayer
    },
        name: 'SongList'
    }
</script>