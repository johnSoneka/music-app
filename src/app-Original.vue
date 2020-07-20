<template>
  <div id="app">
    <!--<div id="nav">
       <img class="logo" alt="Vue logo" src="assets/logo.png" />
      <router-link to="/">Home</router-link> |
      <router-link to="/portofolio">Portofolio</router-link> |
      <router-link to="/service">Service</router-link> |
      <router-link to="/about">Aboffut</router-link>
    </div>
    <router-view /> -->
    <div class="my-all">
      <john />
      <header>
        <h1>My Music Apps</h1>
        <listComponent/>
      </header> 
      
      <!-- the App content-->
      <main>
      <!-- START PLAY LIST -->
        <section class="playList">
          <div class="first-col">
            <h3>Play list</h3>
            <ol>
              <li class="list" v-for="song in songs" :key="song.src" @click="play(song)" :class="song.src == current.src ? 'Song Playing' : 'song'">  
              <a>{{song.title}} - {{song.artist}}</a>
              </li>
            </ol> 
            <input type="file" placeholder="Add a song" value="add" >
          </div>
          <!--Artist details-->
          <div class="second-col">
            <h3 class="song-title">{{current.title}}- <span>{{current.artist}}</span></h3>
          </div>
          <!--END ARTIST DETAILS-->
        </section>
      <!-- eND PLAY LIST-->

      <!--Artist details-->
        <section class="artist-detail">
          <h3 class="song-title">{{current.title}}- <span>{{current.artist}}</span></h3>
        </section>
      <!--END ARTIST DETAILS-->

      <!-- start Control-->
        <section class="control">
          <button class="control-btn prev" @click="prev">Prev</button>
          <button class="control-btn play" v-if="!isPlaying" @click="play">Play</button>
          <button class="control-btn pause" v-else @click="pause">Pause</button>
          <button class="control-btn next" @click="next">Next</button>
        </section>
        <!-- END CONTROL-->
      </main>
    </div>
    
    

  </div>
</template>
<script>
import listComponent from "./components/listComponent.vue"
export default {
  name : 'app',
  data () {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      isRepeating: true,
      songs: [
        {
          title : 'Silence',
          artist: 'Pompi',
          src: require('./assets/silence.mp3')
        },
        {
          title : 'Second Song',
          artist : 'Jay',
          src: require('./assets/Packaging.mp3')
        },
        {
          title : 'Musician',
          artist : 'Jay',
          src: require('./assets/Refuge.mp3')
        },
        {
          title : 'Her love',
          artist : 'Jay',
          src: require('./assets/her.mp3')
        },
         {
          title : 'the lover',
          artist: 'John',
          src: require('./assets/love.mp3')
        }
      ],
      player: new Audio()
    }
  },
  components: {
    listComponent
  },
  methods: {
    repeat () {
      
      this.player.addEventListener('ended', function(){
        this.index;
        this.current = this.songs[this.index];
        this.play(this.current)
      }.bind(this)),
      this.player.play();
      this.isPlaying = true,
      this.isRepeating = false
    },
    norepeat () {
      this.isRepeating = true
    },
    play (song) {
      if(typeof song.src !="undefined"){
        this.current = song;
        this.player.src = this.current.src;

      }
      this.player.play();
      this.player.addEventListener('ended', function(){
         this.index++;
        if(this.index > this.songs.length - 1){
          this.index = 0
        }
        this.current = this.songs[this.index];
        this.play(this.current)
      }.bind(this)),
      this.isPlaying = true
    },
    pause () {
      this.player.pause();
      this.isPlaying = false
    },
    prev () {
      this.index--;
      if(this.index < 0){
        this.index = this.songs.length - 1
      }
      this.current = this.songs[this.index];
      this.play(this.current)
    },
    next () {
      this.index++;
      if(this.index > this.songs.length - 1){
        this.index = 0
      }
      this.current = this.songs[this.index];
      this.play(this.current)
    }
  },
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    
  }
}
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.my-all{
  background: #240303;
  width: 75%;
  margin: auto;
  border-radius: 50px;
  color: #fff;
  header{
  background-color: none;
  }
  //contol buttons
  .control{
    border-radius: 0 0px 50px 50px;
    .control-btn{
      background-color: transparent;
      color: #fff;
      margin: 3px;
      padding: 15px 10px 15px 10px;
      border-radius: 50% 50%;
      border: 2px solid #fff;   
    }
    .next{
     
    }
    .prev{
     
    }
    .pause{
     
    }
    .play{
     
    }
  }
  // END contol buttons
}

a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
}

.playList{
  background-color: aquamarine;
  display: block;
  width: 90%;
  margin: auto;
  text-align: left;
  h3{
    padding: 5px;
    font-size: 28px;
    background-color: #1c1c1c;
  }
  .list{
  display: block;
  }
}
.artist-detail{
  background: lawngreen;
  width: 30%;
}
</style>
