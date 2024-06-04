<script>
  // Function to gradually show text
  function showText(id, delay) {
    setTimeout(() => {
      document.getElementById(id).style.opacity = 1;
    }, delay);
  }

  // Show each text with a delay
  document.addEventListener("DOMContentLoaded", () => {
    showText("text1", 1000); // Show first text after 1 second
    showText("text2", 3000); // Show first text after 1 second
    showText("text3", 5000); // Show first text after 1 second
    showText("text4", 7000); // Show first text after 1 second
    showText("text5", 10000); // Show first text after 1 second
    showText("text6", 13000); // Show first text after 1 second
  });
</script>

<!-- Include Google Font -->
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap" rel="stylesheet">

<section id="intro-section">
  <p class="body-text" id="text1">
    Kobe Bean Bryant (August 23, 1978 – January 26, 2020) was an American professional basketball player.</p>
  <p class="body-text" id="text2">
    He spent his entire 20-year career with the Los Angeles Lakers in the National Basketball Association (NBA).</p>
  <p class="body-text" id="text3">
    Widely regarded as one of the greatest players in the history of the sport, Bryant won five NBA championships and was an 18-time All-Star.</p>
  <p class="body-text" id="text4">
    He also is the 2008 NBA Most Valuable Player (MVP), and a two-time NBA Finals MVP. 
  <p class="body-text" id="text5">
  He was posthumously voted into the Naismith Memorial Basketball Hall of Fame in 2020 and named to the NBA 75th Anniversary Team in 2021.</p>
  <p class="small-text" id="text6">
    In this article, we will analyze Kobe's career in the NBA with detailed scoring statistics across the years, his altering performance with and without certain teammates, comparison to other players with same positions, and his retirement and legacy.
  </p>
  <div id="images-container">
    <img src="public\img\kobe.jpg" alt="Kobe Bryant" class="intro-image"/>
  </div>
</section>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap');
  @import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap');

  body {
    font-family: 'Montserrat', sans-serif;
    margin: 0;
    padding: 0;
    background: linear-gradient(to bottom, #552583, #FDB927); /* Lakers colors */
    color: #333;
  }

  #intro-section {
    max-width: 800px;
    margin: 1rem auto;
    padding: 1rem;
    background: #FDB927; /* Lakers yellow background */
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* 添加阴影提升视觉效果 */
  }

  .body-text {
    font-family: 'Montserrat', sans-serif;
    font-size: 1.2rem;
    line-height: 1.6;
    color: #333;
    text-align: center;
    margin-bottom: 1rem; 
    opacity: 0; 
    transition: opacity 1s ease-in-out; 
  }

  .small-text {
    font-family: 'Montserrat', sans-serif;
    font-size: 1.2rem; 
    line-height: 1.6;
    color: #333;
    text-align: justify;
    font-weight: bold; 
    margin-top: 3rem; 
    margin-bottom: 1rem; 
    opacity: 0; 
    transition: opacity 1s ease-in-out; 
  }

  #images-container {
    display: flex;
    justify-content: center; /* Center the image container */
    padding: 1rem 0; /* Padding to provide some space around the images */
  }

  .intro-image {
    width: 80%; /* Increase the width to make the image larger */
    max-width: 100%; /* Ensure the image does not exceed the container width */
    height: auto;
    border: 2px solid #333; /* Adding a border to enhance the images' appearance */
    border-radius: 4px; /* Rounded corners for images */
  }

  @media screen and (max-width: 950px) {
    .body-text {
      font-size: 1.2rem;
    }

    .small-text {
      font-size: 1rem; /* 在较小屏幕上调整字体大小 */
    }

    #images-container {
      flex-direction: column;
      padding: 1rem 0; /* Adjust padding for smaller screens */
    }

    .intro-image {
      width: 100%; /* Ensure the image takes full width on smaller screens */
      margin-bottom: 1rem;
    }
  }
</style>



















