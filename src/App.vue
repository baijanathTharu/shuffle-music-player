<template>
  <div id="app">
    <header>
      <h1>Shuffle Player</h1>
    </header>
    <main>
      <section class="music-player">
        <div class="wallpaper">
          <img v-bind:src="'/pngs/' + this.currentSong[0].wallpaper" alt />
        </div>
        <div class="details">
          <div class="song-title">
            <h4 class="tracking-in-expand">{{this.currentSong[0].title}}</h4>
          </div>
          <div class="song-artist">
            <h5 class="tracking-in-expand">{{this.currentSong[0].artist}}</h5>
          </div>
        </div>
        <div class="controls">
          <button
            class="previous"
            v-if="isPlayArrayLengthGreaterThanOne"
            @click="prevAudio"
          >Previous</button>
          <button class="play" v-if="!isPlaying" @click="playAudio">Play</button>
          <button class="pause" v-else @click="pauseAudio">Pause</button>
          <button class="next" @click="nextAudio">Next</button>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      randNum() {
        const numberOfSongs = 3;
        return Math.floor(Math.random() * numberOfSongs);
      },
      isPlaying: false,
      isPlayArrayLengthGreaterThanOne: false,
      songs: [
        {
          id: 0,
          title: "Isara",
          artist: "Eluvetie",
          wallpaper: "0.png",
        },
        {
          id: 1,
          title: "Music One",
          artist: "Unknown",
          wallpaper: "1.jpg",
        },
        {
          id: 2,
          title: "Music Two",
          artist: "Unknown",
          wallpaper: "2.jpg",
        },
        {
          id: 3,
          title: "Heart Like a Grave",
          artist: "Insomnium",
          wallpaper: "3.jpg",
        },
        {
          id: 4,
          title: "The Eagle Flies Alone",
          artist: "Arch Enemy",
          wallpaper: "4.jpg",
        },
        {
          id: 5,
          title: "Shadows of the Dying Sun",
          artist: "Insomnium",
          wallpaper: "5.jpg",
        },
        {
          id: 6,
          title: "Lose to Night",
          artist: "Insomnium",
          wallpaper: "6.jpg",
        },
        {
          id: 7,
          title: "While We Sleep",
          artist: "Insomnium",
          wallpaper: "7.jpg",
        },
        {
          id: 8,
          title: "The Promethean Song",
          artist: "Insomnium",
          wallpaper: "8.jpg",
        },
      ],
      currentSong: [
        {
          id: 0,
          title: "Isara",
          artist: "Eluvetie",
          wallpaper: "0.png",
        },
      ],
      playArray: [
        {
          id: 0,
          title: "Isara",
          artist: "Eluvetie",
          wallpaper: "0.png",
        },
      ],
      audioObj: new Audio(require(`./assets/files/0.mp3`)),
    };
  },
  created: function () {},
  methods: {
    playAudio() {
      this.isPlaying = true;
      this.audioObj.play();
    },
    pauseAudio() {
      this.isPlaying = false;
      this.audioObj.pause();
    },
    nextAudio() {
      let randomSong = this.randNum();
      while (randomSong === this.currentSong[0].id) {
        randomSong = this.randNum();
      }
      this.audioObj.src = require(`./assets/files/${randomSong}.mp3`);
      this.playArray.push(this.songs[randomSong]);
      this.currentSong.splice(0, 1, this.songs[randomSong]);
      this.isPlayArrayLengthGreaterThanOne = true;
      this.audioObj.play();
    },
    prevAudio() {
      const songId =
        this.playArray[this.playArray.length - 2].id < 0
          ? 0
          : this.playArray[this.playArray.length - 2].id;
      this.audioObj.src = require(`./assets/files/${songId}.mp3`);
      this.isPlaying = true;
      this.playArray.push(this.songs[songId]);
      this.currentSong.splice(0, 1, this.songs[songId]);
      this.audioObj.play();
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: sans-serif;
}
header {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgb(0, 0, 0);
}

header h1 {
  color: white;
  padding: 20px;
  font-size: 24px;
  font-weight: 400;
}

.music-player {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: lightgrey;
}

.wallpaper {
  /* background: teal; */
  margin: 10px 0px;
}

.wallpaper img {
  width: 250px;
  height: 250px;
  border: 1px solid black;
  border-radius: 180px;
}

.details {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 20px;
}

.song-title h4 {
  color: black;
  padding: 10px;
  font-size: 24px;
}

.tracking-in-expand {
  -webkit-animation: tracking-in-expand 4s cubic-bezier(0.39, 0.575, 0.565, 1)
    infinite both;
  animation: tracking-in-expand 4s cubic-bezier(0.39, 0.575, 0.565, 1) infinite
    both;
}

@-webkit-keyframes tracking-in-expand {
  0% {
    letter-spacing: -0.5em;
    opacity: 0;
  }
  40% {
    opacity: 0.6;
  }
  100% {
    opacity: 1;
  }
}
@keyframes tracking-in-expand {
  0% {
    letter-spacing: -0.5em;
    opacity: 0;
  }
  40% {
    opacity: 0.6;
  }
  100% {
    opacity: 1;
  }
}

.song-artist h5 {
  color: black;
  padding: 10px;
  font-size: 16px;
}

.controls {
  display: flex;
  justify-content: space-between;
  align-items: center;
  /* border: 1px solid black; */
  padding: 10px;
}

.controls button {
  margin: 10px;
  padding: 10px;
  font-size: 15px;
  background-color: rgb(0, 0, 0, 0.85);
  color: white;
  outline: none;
  border: none;
  z-index: 5;
}
.controls button:hover {
  cursor: pointer;
  background-color: rgb(0, 0, 0);
}
</style>
