<script>
    let isPlaying = true;
    let audio;
  
    function togglePlayPause() {
      if (isPlaying) {
        audio.pause();
      } else {
        audio.play();
      }
      isPlaying = !isPlaying;
    }
  </script>
  
  <audio bind:this={audio} autoplay loop>
    <source src="src\audio\music.mp3" type="audio/mpeg">
    Your browser does not support the audio element.
  </audio>
  
  <button on:click={togglePlayPause}>
    {isPlaying ? 'Pause' : 'Play'}
  </button>
  
  <style>
    button {
      position: fixed;
      top: 10px;
      right: 10px;
      padding: 10px;
      background-color: #f0f0f0;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #e0e0e0;
    }
  </style>
  