<section id="conclusion">
  <h1 class="body-header">Concluding Text</h1>
  <p class="body-text" id="conclusion-text">
    Known for his scoring prowess, relentless work ethic, and clutch performances, Kobe won five NBA championships, earned two Finals MVP awards, and was an 18-time All-Star. His career totals include over 33,000 points, ranking him among the top scorers in NBA history. Kobe's influence extended beyond the court, inspiring countless athletes worldwide.
  </p>
</section>

<script>
  // Function to show text with blinking effect once
  function showText(id, delay) {
    setTimeout(() => {
      var element = document.getElementById(id);
      element.style.opacity = 1;
      setTimeout(() => {
        element.style.opacity = 0;
        setTimeout(() => {
          element.style.opacity = 1;
        }, 500); // Blink off for 0.5 seconds
      }, 500); // Blink on for 0.5 seconds
    }, delay);
  }

  // Function to show image with blinking effect once
  function showImage(id, delay) {
    setTimeout(() => {
      var element = document.getElementById(id);
      element.style.opacity = 1;
      setTimeout(() => {
        element.style.opacity = 0;
        setTimeout(() => {
          element.style.opacity = 1;
        }, 500); // Blink off for 0.5 seconds
      }, 500); // Blink on for 0.5 seconds
    }, delay);
  }

  // Append the image to the document body after the conclusion section
  document.addEventListener("DOMContentLoaded", () => {
    var conclusionSection = document.getElementById('conclusion');
    
    var image = document.createElement('img');
    image.src = "./Kobe-career/public/assets/img/end.jpg";
    image.alt = 'Kobe Bryant';
    image.style.width = '80%';
    image.style.maxWidth = '100%';
    image.style.height = 'auto';
    image.style.border = '2px solid #333';
    image.style.borderRadius = '4px';
    image.style.opacity = '0'; // Initial hidden state
    image.style.transition = 'opacity 1s ease-in-out';
    image.style.margin = '1rem auto';
    image.style.display = 'block'; // Center the image horizontally
    image.id = 'conclusion-image';

    // Append the image after the conclusion section
    conclusionSection.insertAdjacentElement('afterend', image);
    
    // Show the text and then the image with delays
    showText("conclusion-text", 1000); // Show text after 1 second
    showImage("conclusion-image", 3000); // Show image after 3 seconds (after the text has blinked)
  });
</script>

<style>
#conclusion {
  padding: 2rem 1rem;
}

#references {
  padding: 2rem 1rem;
}

.body-header {
  font-size: 1.5rem;
  font-weight: bold;
}

.body-text {
  font-size: 1rem;
  line-height: 1.5;
  opacity: 0; /* Initial hidden state */
  transition: opacity 1s ease-in-out; /* Transition effect */
}

#references ul {
  list-style-type: none;
  padding: 0;
}

#references li {
  margin-bottom: 0.5rem;
}

#references a {
  color: blue;
  text-decoration: underline;
}
</style>




