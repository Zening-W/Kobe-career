<script>
  import a from '/assets/audio/music.mp3';
  let isPlaying = true;
  let audio;

  function togglePlayPause() {
    if (audio) {
      if (audio.paused) {
        audio.play();
        isPlaying = true;
      } else {
        audio.pause();
        isPlaying = false;
      }
    }
  }

  function onAudioLoaded() {
    if (audio) {
      audio.play().then(() => {
        isPlaying = true;
      }).catch((error) => {
        isPlaying = false;
        console.error("Autoplay was prevented:", error);
      });
    }
  }
</script>

<audio bind:this={audio} on:canplay={onAudioLoaded} autoplay loop>
  <source src={a} />

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
