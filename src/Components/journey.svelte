<script>
  document.addEventListener("DOMContentLoaded", function () {
    const style = document.createElement('style');
    style.innerHTML = `
      @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap');

      body {
        font-family: 'Montserrat', sans-serif;
        margin: 0;
        padding: 0;
        background: linear-gradient(to bottom, #552583, #FDB927); /* Lakers colors */
        color: #333;
      }

      #journey-section {
        max-width: 800px;
        margin: 1rem auto;
        padding: 1rem;
        background: none;
        transition: background 1s ease-in-out, color 1s ease-in-out;
      }

      .journey-text {
        font-size: 1.2rem;
        line-height: 1.6;
        color: #333;
        text-align: justify;
        margin-bottom: 1rem;
      }

      .background-visible {
        background: linear-gradient(to bottom, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url('src/img/kobe.jpg') no-repeat center center;
        background-size: cover;
        color: #fff;
        padding: 4rem;
        border-radius: 8px;
      }
    `;
    document.head.appendChild(style);

    function handleScroll() {
      const sectionTop = journeySection.getBoundingClientRect().top;
      const triggerPoint = window.innerHeight / 1.5; // Adjust trigger point as needed

      if (sectionTop < triggerPoint) {
        journeySection.classList.add('background-visible');
      } else {
        journeySection.classList.remove('background-visible');
      }
    }

    window.addEventListener('scroll', handleScroll);

    handleScroll();
  });
</script>




