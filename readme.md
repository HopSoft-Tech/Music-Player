# Music Player App

A simple, elegant music player application that allows you to play, pause, and switch between songs. This project showcases basic JavaScript functionalities and DOM manipulation techniques.

## Features

- Play and pause songs
- Skip to the next or previous song
- Visual progress bar that updates as the song plays
- Clickable progress bar to jump to different parts of the song
- Dynamic song and cover image loading

## Demo

![Music Player Screenshot](images/ukulele.jpg)

## Getting Started

### Prerequisites

To run this project locally, you need a web browser and a local server environment or simply open the `index.html` file directly in your browser.

### Installation

1. Clone the repository:

   ```sh
   git clone https://github.com/HopSoft-Tech/music-player.git
   ```

2. Navigate to the project directory:

   ```sh
   cd music-player
   ```

3. Open the `index.html` file in your browser:

   ```sh
   open index.html
   ```

### Project Structure

```
music-player/
├── images/
│   ├── hey.jpg
│   ├── summer.jpg
│   ├── ukulele.jpg
│   └── fallingdown.jpg
├── music/
│   ├── hey.mp3
│   ├── summer.mp3
│   ├── ukulele.mp3
│   └── fallingdown.mp3
├── app.js
├── index.html
└── style.css
```

### Code Overview

#### HTML

The HTML structure provides the layout for the music player, including the song title, progress bar, cover image, and control buttons.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <link rel="stylesheet" href="style.css" />
    <script src="app.js" defer></script>
    <title>Music Player</title>
  </head>
  <body>
    <h1>Music Player</h1>
    <div class="music-container" id="music-container">
      <div class="music-info">
        <h4 id="title"></h4>
        <div class="progress-container" id="progress-container">
          <div class="progress" id="progress"></div>
        </div>
      </div>
      <audio src="music/ukulele.mp3" id="audio"></audio>
      <div class="img-container">
        <img src="images/ukulele.jpg" alt="music-cover" id="cover" />
      </div>
      <div class="navigation">
        <button id="prev" class="action-btn">
          <i class="fas fa-backward"></i>
        </button>
        <button id="play" class="action-btn action-btn-big">
          <i class="fas fa-play"></i>
        </button>
        <button id="next" class="action-btn">
          <i class="fas fa-forward"></i>
        </button>
      </div>
    </div>
  </body>
</html>
```

#### CSS

The CSS file (`style.css`) styles the music player, making it visually appealing and responsive.

#### JavaScript

The JavaScript file (`app.js`) contains the core logic of the music player, including play/pause functionality, song switching, and progress bar updates.

```javascript
const musicContainer = document.getElementById("music-container");
const playBtn = document.getElementById("play");
const prevBtn = document.getElementById("prev");
const nextBtn = document.getElementById("next");
const audio = document.getElementById("audio");
const progress = document.getElementById("progress");
const progressContainer = document.getElementById("progress-container");
const title = document.getElementById("title");
const cover = document.getElementById("cover");

// Song titles
const songs = ["hey", "summer", "ukulele", "fallingdown"];

// Keep track of song
let songIndex = 0;

// Initially load song details into DOM
loadSong(songs[songIndex]);

// Update song details
function loadSong(song) {
  title.innerText = song;
  audio.src = `music/${song}.mp3`;
  cover.src = `images/${song}.jpg`;
}

// Play song
function playSong() {
  musicContainer.classList.add("play");
  playBtn.querySelector("i.fas").classList.remove("fa-play");
  playBtn.querySelector("i.fas").classList.add("fa-pause");
  audio.play();
}

// Pause song
function pauseSong() {
  musicContainer.classList.remove("play");
  playBtn.querySelector("i.fas").classList.add("fa-play");
  playBtn.querySelector("i.fas").classList.remove("fa-pause");
  audio.pause();
}

// Previous song
function prevSong() {
  songIndex--;

  if (songIndex < 0) {
    songIndex = songs.length - 1;
  }

  loadSong(songs[songIndex]);
  playSong();
}

// Next song
function nextSong() {
  songIndex++;

  if (songIndex > songs.length - 1) {
    songIndex = 0;
  }

  loadSong(songs[songIndex]);
  playSong();
}

// Update progress bar
function updateProgress(e) {
  const { duration, currentTime } = e.srcElement;
  const progressPercent = (currentTime / duration) * 100;
  progress.style.width = `${progressPercent}%`;
}

// Set progress bar
function setProgress(e) {
  const width = this.clientWidth;
  const clickX = e.offsetX;
  const duration = audio.duration;

  audio.currentTime = (clickX / width) * duration;
}

// Event listeners
playBtn.addEventListener("click", () => {
  const isPlaying = musicContainer.classList.contains("play");

  if (isPlaying) {
    pauseSong();
  } else {
    playSong();
  }
});

prevBtn.addEventListener("click", prevSong);
nextBtn.addEventListener("click", nextSong);
audio.addEventListener("timeupdate", updateProgress);
progressContainer.addEventListener("click", setProgress);
```

## Contributing

Feel free to contribute to this project by submitting issues or pull requests.

1. Fork the repository.
2. Create a new branch.
3. Make your changes and commit them.
4. Push to the branch.
5. Open a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
