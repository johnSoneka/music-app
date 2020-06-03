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
    <header>
      <h1>My Music Apps</h1>
    </header> 
    <main>
      <section class="player">
        <h3 class="song-title">{{current.title}}- <span>{{current.artist}}</span></h3>
        
      </section>
      <div class="contro">
        <button class="prev" @click="prev">Prev</button>
        <button class="play" v-if="!isPlaying" @click="play">Play</button>
        <button class="pause" v-else @click="pause">Pause</button>
        <button class="next" @click="next">Next</button>
        <button class="next" v-if="isRepeating" @click="repeat">repeat</button>
        <button class="next" v-else @click="norepeat">no-repeat</button>
      </div>
      <section class="playList">
        <h3>Play list</h3>
        <ol>
          <li class="list" v-for="song in songs" :key="song.src" @click="play(song)" :class="song.src == current.src ? 'Song Playing' : 'song'">
            
        <a>{{song.title}} - {{song.artist}}</a>
          </li>
        </ol>
        
      </section>
    </main>

  </div>
</template>
<script>
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
          title : 'Her love',
          artist : 'Jay',
          src: require('./assets/her.mp3')
        },
        {
          title : 'Her love',
          artist : 'Jay',
          src: require('./assets/her.mp3')
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

#nav {
  top: 0%;

  padding: 0px;
  background-color: aqua ;
  .logo {
    width: 30px;
    height: 30px;
    background-image:url(assets/logo.png);
    padding: 10px;
    margin-right: 100px;
  }
  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
header{
  background-color: #1c1c1c;
  color: #c1c1c1;

}
.next{
  background-color: green;
  border-radius: 0 50% 50% 0;
  padding: 15px 10px 15px 10px;
  color: #fff;
}
.prev{
  background-color: green;
  border-radius: 50% 0 0 50%;
  padding: 15px 10px 15px 10px;
  color: #fff;
}
.pause{
  background-color: red;
  color: #fff;
  border-radius: 50%;
  padding: 15px 10px 15px 10px;
}
.play{
  background-color: blue;
  border-radius: 50%;
  color: #fff;
  padding: 15px 10px 15px 10px;
}
.playList{
  background-color: aquamarine;
  padding: 0 10px;
  text-align: center;
}
.list{
  text-align: center;
  display: block;
  color: red;
}
</style>
