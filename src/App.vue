<template>
  <div id="app">
    <header>
      <h1>My Music App</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">{{current.title}} - <span>{{current.artist}}</span> </h2>
        <div class="controls">
          <button class="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" @click="pause" v-else>Pause</button>
          <button class="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>Your Playlist</h3>
        <button v-for="song in songs" :key="song" @click="play(song)" :class="(song.src == current.src) ? 'song playing' : 'song'">
          {{ song.title}} - {{song.artist}}
        </button>
      </section>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return{
      current: { },
      isPlaying: false,
      index: 0,
      songs: [
        {
          title: 'Grateful',
          artist: 'Don Meon',
          src: require('./assets/donmeon.mp3')
        },
        {
          title: 'Kylie Grace',
          artist: 'Grace',
          src: require('./assets/lookatme.mp3')
        }
      ],
      player: new Audio()
    }
  },
  methods: {
    play (song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },
    pause () {
      this.player.pause();
      this.isPlaying = false;
    }
  },
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    // this.player.play();
  }

}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body{
  font-family: san-serif;
}
header{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #FFF;
}
</style>
