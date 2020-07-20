<template>
    <div>
        <H1>johnny</H1>
        <ol>
              <li class="list" v-for="song in songs" :key="song.src" @click="play(song)" :class="song.src == current.src ? 'Song Playing' : 'song'">  
              <a>{{song.title}}</a>
              </li>
            </ol> 
        <h2>the song is {{song.title}}</h2>
        <!-- START PLAY LIST --
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
          --Artist details--
          <div class="second-col">
            <h3 class="song-title">{{current.title}}- <span>{{current.artist}}</span></h3>
          </div>
          --END ARTIST DETAILS--
        </section>
      -- eND PLAY LIST-->
    </div>
</template>
<script>
export default {
     props: {
        mySongs: {
            type: Array,
            default: function(){
                return{
                    songs: [
                    {
                    title : 'Silence',
                    artist: 'Pompi',
                    src: require('../assets/silence.mp3')
                    }]
                }
            }
        }
     }
}
</script>

<style lang="scss" scoped>
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