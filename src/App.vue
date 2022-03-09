<script setup>
import { GamepadListener } from 'gamepad.js';
import { Howl, Howler } from 'howler';
const listener = new GamepadListener( /* options*/);

var playerFactory = {
  create(file) {
    return new Howl({
      src: file,
      html5: true,
      format: ['mp3', 'wav'],
      onloaderror: (err) => {
        console.error(err)
      }
    })

  }
}

var kickPlayer = playerFactory.create('./samples/kick-softy.mp3');
var snarePlayer = playerFactory.create('./samples/snare-acoustic02.mp3');
var hihatPlayer = playerFactory.create('./samples/hihat-acoustic02.mp3');
var openHatPlayer = playerFactory.create('./samples/openhat-acoustic01.mp3');
var tomPlayer = playerFactory.create('./samples/tom-acoustic01.mp3');

var drums = {
  kick() {
    console.log('kick')
    kickPlayer.play()
  },

  snare() {
    console.log('snare')
    snarePlayer.play()
  },

  hihat() {
    console.log('hihat')
    hihatPlayer.play()
  },

  openHat() {
    console.log('hihat');
    openHatPlayer.play();
  },

  tom() {
    console.log('hihat');
    tomPlayer.play();
  }
}


listener.start();


listener.on('gamepad:connected', function (event) {
  console.log('Gamepade connected')
});

listener.on('gamepad:disconnected', function (event) {
  console.log('Gamepade disconnected')
});

// listener.on('gamepad:0:button', function(event) {
//     console.log('Button: A pressed')
// });
listener.on('gamepad:0:button:0', function (event) {
  if (event.detail.pressed) {
    drums.kick();
  }
});
listener.on('gamepad:0:button:1', function (event) {
  if (event.detail.pressed) {
    drums.snare();
  }
});

listener.on('gamepad:0:button:2', function (event) {
  if (event.detail.pressed) {
    drums.hihat();
  }
});
listener.on('gamepad:0:button:3', function (event) {
  if (event.detail.pressed) {
    drums.tom();
  }
});
</script>

<template>
  <div class="container">
    <h1>Launchtron</h1>
    <div class="item">
      <select>
        <option value="0"> A Button</option>
        <option value="1"> B Button</option>
        <option value="2"> X Button</option>
        <option value="3"> Y Button</option>
      </select>
      <br>
      <button class="pad" @click="drums.kick">Kick</button>
    </div>
    <div class="item">
      <select>
        <option value="0"> A Button</option>
        <option value="1"> B Button</option>
        <option value="2"> X Button</option>
        <option value="3"> Y Button</option>
      </select>
      <br>
      <button class="pad" @click="drums.snare">Snare</button>
    </div>
    <div class="item">
      <select>
        <option value="0"> A Button</option>
        <option value="1"> B Button</option>
        <option value="2"> X Button</option>
        <option value="3"> Y Button</option>
      </select>
      <br>
      <button class="pad" @click="drums.hihat">Hi-Hat</button>
    </div>
    <div class="item">
      <select>
        <option value="0"> A Button</option>
        <option value="1"> B Button</option>
        <option value="2"> X Button</option>
        <option value="3"> Y Button</option>
      </select>
      <br>
      <button class="pad" @click="drums.openHat">Hi-Hat Open</button>
    </div>
    <div class="item">
      <select>
        <option value="0"> A Button</option>
        <option value="1"> B Button</option>
        <option value="2"> X Button</option>
        <option value="3"> Y Button</option>
      </select>
      <br>
      <button class="pad" @click="drums.tom">Tom</button>
    </div>
  </div>
</template>

<style>
.container {
  flex-flow: row wrap;
   justify-content: flex-start;
   align-content: space-between;
   gap: 10px;
   box-sizing: border-box;
}
.item{
  flex-basis: auto
}

.pad {
  background-color: cornflowerblue;
  border: none;
  color: white;
  font-size: large;
}
</style>
