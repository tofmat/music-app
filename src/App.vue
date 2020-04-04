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
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next">Next</button>
        </div>
      </section>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  isPlaying: false,
  data () {
    return{
      current: { },
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
    play(song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }

      this.player.play();
      this.isPlaying = false;
    },
    pause () {
      this.player.pause();
      this.isPlaying = true;
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
