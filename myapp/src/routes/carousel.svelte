<script>
    import PrevButton from "./leftnavbutton.svelte";
    import NextButton from "./rightnavbutton.svelte";
    let progress = 0;

    let currentSlide = 0;
    let slides = [
      {
        image: 'src/images/app.png',
        // ResizeObserverSize,
        caption: 'Vehicle Ownership Starts Here'
      },
      {
        image: 'src/images/maintenance.png',
        // ResizeObserverSize,
        caption: 'Free Vehicle Health Report'
      },
      {
        image: 'src/images/roadside.png',
        // ResizeObserverSize,
        caption: 'Roadside Assistance'
      }
    ];
  
    function nextSlide() {
      currentSlide = (currentSlide + 1) % slides.length;
      advanceProgress();
    }
  
    function prevSlide() {
      currentSlide = (currentSlide - 1 + slides.length) % slides.length;
      decreaseProgress();
    }

    function advanceProgress() {
        progress = Math.min(100, progress + (100 / slides.length));
    }

    function decreaseProgress() {
        progress = Math.max(0, progress - (100 / slides.length));
    }
  </script>
  
  <style>
    .carousel {
      display: flex;
      width:100%;
    }

    .carousel img {
      width: 31.4rem;
      height: 35em;
    }
  
    .slide {
      flex: 1;
    }
  
    .slide-caption {
      font-size: 18px;
      font-weight: bold;
      text-align: center;
    }

    .progress-bar {
    width: 25rem; /* set the initial width of the progress bar */
    height: 1rem;
    background-color: #868686;
    border-radius: 10px;
    margin-right: 10rem;
  }

  .progress-bar-fill {
    height: 100%;
    background-color: #3D6889;
    border-radius: 10px;
    transition: width 0.5s; /* add a transition effect when the width changes */
  }


  </style>

<div class="carousel">
    <PrevButton on:click={prevSlide}></PrevButton>
    <div class="slide">
      <img class="slide-image" src={slides[currentSlide].image} alt="" />
      <p class="slide-caption">{slides[currentSlide].caption}</p>
    </div>
    <NextButton on:click={nextSlide}></NextButton>
  </div>
  <div class="progress-bar">
    <div class="progress-bar-fill" style={`width: ${progress}%`}></div>
  </div>