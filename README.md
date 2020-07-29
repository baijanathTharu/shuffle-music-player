# Shuffle Player

This is music player which plays music in random order. You can see the demo [here](https://bntharu.com.np/projects/shuffle-player).

---

## Project setup

```
npm install
```

### Compiles and hot-reloads for development

```
npm run serve
```

### Compiles and minifies for production

```
npm run build
```

##Instructions
I have added three songs and you can try it without doing anything at all but if you want to play your songs then you must follow following steps.

1. Rename each mp3 file that you want to play in number. For e.g. 0.mp3, 1.mp3, 2.mp3 and so on in increasing order.
1. Place the mp3 files in the /src/assets/files directory.
1. Place the wallpapers of each image in /public/pngs directory.

1. In App.vue file, Change the value of the variable "numberOfSongs" to one greater than the number of songs you added on line 40.

```
  const numberOfSongs = NumberofSongsYouAdded + 1;
```

1. In App.vue file, edit the "songs" object according to the songs you have added. For e.g:

```
songs: [
  {
    id: 0,
    title: "Title of your song",
    artist: "Artist of the song",
    wallpaper: "wallpaper-name.extension-name",
  },
  {
    id: 1,
    title: "Title of your song",
    artist: "Artist of the song",
    wallpaper: "wallpaper-name.extension-name",
  },
];
```
