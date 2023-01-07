
<script>
// @ts-nocheck

    import Header from './Header.svelte';
    import Footer from './Footer.svelte';
    import './stylesheet.css';
    import PrevButton from "./leftnavbutton.svelte";
    import NextButton from "./rightnavbutton.svelte";
    import {slide, fade} from 'svelte/transition';
    import {elasticInOut} from 'svelte/easing';
    import roadsideImage from "./roadside3.png";
    import welcome_fallback from './svelte-welcome.png';
    import vehicleService from './service.png';
    import healthReport from './reportimage.png';
    // import HealthServicesButton from './healthservice.svelte';
	  // import HealthReport from './healthreport.svelte';
	  // import Roadside from './roadsidebutton.svelte';
    // import CrashDetect from './crashdetect.svelte';
    // import VoiceAssistant from './voiceassistant.svelte';
    import { createEventDispatcher, onDestroy } from 'svelte';
    // import { onMount } from "svelte";
	  // import { null_to_empty, set_input_type } from 'svelte/internal';
    let progress = 0;

    let currentSlide = 0;
    let counter = 0;
    let timer;

    let slides = [
      {
        image: './firstimage.png',
        // ResizeObserverSize,
        caption: 'Me and My Car'
      },
      {
        image: './secondimage.png',
        // ResizeObserverSize,
        caption: 'Free Vehicle Health Report'
      },
      {
        image: './thirdimage.png',
        // ResizeObserverSize,
        caption: 'Roadside Assistance'
      },
      {
        image: './fourthimage.png',
        // ResizeObserverSize,
        caption: 'Car Crash Detection'
      },
      {
        image: './fifthimage.png',
        // ResizeObserverSize,
        caption: 'Car Maintenance Service'
      }
    ];
    // let slide = 0;
    
  //   let slides = [
  //   './firstimage.png',
  //   './secondimage.png',
  //   './thirdimage.png',
  //   './fourthimage.png',
  //   './fifthimage.png'
  // ];

    function startTimer() {
      timer = setInterval(() => {
        // Go to the next slide
        currentSlide = (currentSlide + 1) % slides.length;
      }, 3000); // 3 seconds
  }

    // Stop the timer
    function stopTimer() {
    // @ts-ignore
    clearInterval(timer);
  }

  startTimer();
  
  function nextSlide() {
      if (currentSlide  == 4){
        currentSlide = 0;
        progress = 0;
      }
      else{
        currentSlide = (currentSlide + 1) % slides.length;
        advanceProgress();
        counter += 1;
      }
    }
  
    function prevSlide() {
      if (currentSlide != 0){
        currentSlide = (currentSlide - 1 + slides.length) % slides.length;
        decreaseProgress();
        counter -= 1;
      }
      else{
        currentSlide = slides.length - 1;
      }
    }
    function advanceProgress() {
        if (progress == 4){
          progress = Math.min(100, 0 + (100 / slides.length));
        }
        else{
          progress = Math.min(100, progress + (100 / slides.length));
        }
    }
    function decreaseProgress() {
        if (progress == 0){
          progress = Math.min(100, 80 + (100 / slides.length));
        }
        else{
          progress = Math.max(0, progress - (100 / slides.length));
        }
    }

    // function restart(){
    //   progress = 0;
    // }

    let scroll_progress = 0;

// window.addEventListener('scroll', () => {
//   requestAnimationFrame(() => {
//     scroll_progress = (100 * window.scrollY) / (document.body.scrollHeight - window.innerHeight);
//   });
// });
  let active = false;
  let text = '';
  const click = '';
  let toggle = 'true';

  let shown = false;
  let shown1 = false;
  let shown2 = false;
  let shown3 = false;
	
  let dispatch = createEventDispatcher();

  function show() {
      shown = !shown;
      dispatch('show', shown);
  }

  function show1() {
      shown1 = !shown1;
      dispatch('show1', shown1);
  }

  function show2() {
      shown2 = !shown2;
      dispatch('show2', shown2);
  }

  function show3() {
      shown3 = !shown3;
      dispatch('show3', shown3);
  }

// These values are bound to properties of the video
let time = 0;
	// @ts-ignore
	let duration;
	let paused = true;

	let showControls = true;
	// @ts-ignore
	let showControlsTimeout;

	// Used to track time of last mouse down event
	// @ts-ignore
	let lastMouseDown;

	// @ts-ignore
	function handleMove(e) {
		// Make the controls visible, but fade out after
		// 2.5 seconds of inactivity
		// @ts-ignore
		clearTimeout(showControlsTimeout);
		showControlsTimeout = setTimeout(() => showControls = false, 2500);
		showControls = true;

		// @ts-ignore
		if (!duration) return; // video not loaded yet
		if (e.type !== 'touchmove' && !(e.buttons & 1)) return; // mouse not down

		const clientX = e.type === 'touchmove' ? e.touches[0].clientX : e.clientX;
		// @ts-ignore
		const { left, right } = this.getBoundingClientRect();
		time = duration * (clientX - left) / (right - left);
	}

	// we can't rely on the built-in click event, because it fires
	// after a drag — we have to listen for clicks ourselves
	// @ts-ignore
	function handleMousedown(e) {
		lastMouseDown = new Date();
	}

	// @ts-ignore
	function handleMouseup(e) {
		// @ts-ignore
		if (new Date() - lastMouseDown < 300) {
			if (paused) e.target.play();
			else e.target.pause();
		}
	}

	// @ts-ignore
	function format(seconds) {
		if (isNaN(seconds)) return '...';

		const minutes = Math.floor(seconds / 60);
		seconds = Math.floor(seconds % 60);
		if (seconds < 10) seconds = '0' + seconds;

		return `${minutes}:${seconds}`;
	}


  function scrollToElement() {
    // Get the element that you want to scroll to
    let element = document.querySelector('#scroll-target');

    // Scroll the element into view
    // @ts-ignore
    element.scrollIntoView({
      behavior: 'smooth', // Scroll smoothly
      block: 'start', // Align the element at the top of the viewport
      inline: 'nearest' // Align the element to the nearest edge
    });
  }

  function scrollToElement1() {
    // Get the element that you want to scroll to
    let element = document.querySelector('#scroll-target1');

    // Scroll the element into view
    // @ts-ignore
    element.scrollIntoView({
      behavior: 'smooth', // Scroll smoothly
      block: 'start', // Align the element at the top of the viewport
      inline: 'nearest' // Align the element to the nearest edge
    });
  }

</script>

{#if toggle == 'true'}
<button class:active="{active}" on:click="{() => active = !active}">{text}</button>
{:else}
<button on:click="{() => active = !active}">{text}</button>
{/if}

<svelte:options accessors={true}/>

<div class="container">

    <div class="header">
        <p><Header/></p>
    </div>

    <div class="carousel">

        <div class="prev-button">
        <PrevButton on:click={prevSlide}></PrevButton>
        </div>

        <div class="slide" style="transform: translateX({slides * -100}%)">
          
          <img in:slide="{{ duration: 500, easing: elasticInOut}}" out:fade src={slides[currentSlide].image} alt="" width={1000} height={600}/>
          <p class="slide-caption">{slides[currentSlide].caption}</p>
        </div>

        <div class="next-button">
        <NextButton on:click={nextSlide}></NextButton>
        </div>

    </div>

    <!-- <div class="carousel">
      <div class="carousel-slides" style="transform: translateX({slide * -100}%)">
        {#each slides as slide}
          <div class="carousel-slide"><img src={slide} /></div>
        {/each}
      </div>
      <div class="carousel-controls">
        {#each slides as slide, i}
          <div class="carousel-control {i === currentSlide ? 'active' : ''}" on:click={() => goToSlide(i)}>{i + 1}</div>
        {/each}
      </div>
    </div> -->

      <div class="progress-bar">

        <div class="progress-bar-fill" style={`width: ${progress}%`}></div>
        
      </div>
      {#if slide == 0}
      <h3> 00 01</h3>
      {:else if slide == 1}
      <h3> 01 02</h3>
      {:else if slide == 2}
      <h3> 02 03</h3>
      {:else if slide == 3}
      <h3> 03 04 </h3>
      {:else if slide == 4} 
      <h3> 04 04 </h3>
      {/if}

    <div id="scroll-target1">   
    <div class="second-section">
      <!-- <div class="scroll-progress-bar">
        <div class="scroll-progress" style={`height: ${scroll_progress}%`}></div>
    </div> -->
    <div class="benefits-section" id="my-div">
      <li>
      <!-- svelte-ignore a11y-invalid-attribute -->
      <a  href="javascript:void(0)"  class="scroll-link" on:click={scrollToElement1}>Benefits for you</a>
      <br>
      <!-- svelte-ignore a11y-invalid-attribute -->
      <a  href="javascript:void(0)"  class="scroll-link" on:click={scrollToElement}>On-demand services</a>
     </li>
      <h4> Want to know more? </h4>
      <h5> Download and try it out to see how <br> amazing it is. It's free!</h5>
      <button on:click>
        Download
      </button>
    </div>
      <h1>
        Benefits
      </h1>
      <h2>
        We've Got Your Back.
      </h2>
      <div class="paragraph">
      <p> Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor <br> invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et
        <br> accusam et justo duo dolores et ea rebum. </p>
      </div>
      <div class="first-three-buttons">
        <div class="roadside-button">
          <button on:click={show}></button>
          <span>Roadside Assistance</span>
        </div>
        <div class="healthservice-button">
          <button on:click={show}></button>
          <span>Vehicle Health Services</span>
        </div>
        <div class="healthreport-button">
          <button on:click={show}></button>
          <span>Vehicle Health Report</span>
        </div>
      </div>
      {#if shown}
        <p>This is the paragraph of text that will be displayed when you click the button.</p>
      {/if}
    </div>
    </div>

    <div class="third-section">
      <h1>
        Benefits
      </h1>
      <h2>
        Safety.
      </h2>
      <div class="paragraph">
      <p> Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor <br> invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et
        <br> accusam et justo duo dolores et ea rebum. </p>
      </div>
      <div class="two-buttons">
        <div class="crashdetection-button">
          <button on:click={show1}></button>
          <span>Crash Detection</span>
        </div>
        <div class="voiceassistant-button">
          <button on:click={show1}></button>
          <span>Voice Assistant</span>
        </div>
      </div>
      {#if shown1}
      <p>This is the paragraph of text that will be displayed when you click the button.</p>
      {/if}
    </div>

    <div class="fourth-section">
      <h1>
        Benefits
      </h1>
      <h2>
        Save You Time.
      </h2>
      <div class="paragraph">
      <p> Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor <br> invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et
        <br> accusam et justo duo dolores et ea rebum. </p>
      </div>
      <div class="third-three-buttons">
        <div class="coupons-button">
          <button on:click={show2}></button>
          <span>Coupons</span>
        </div>
        <div class="tools-button">
          <button on:click={show2}></button>
          <span>Tools</span>
        </div>
        <div class="tco-button">
          <button on:click={show2}></button>
          <span>Total Cost of Ownership</span>
        </div>
      </div>
      {#if shown2}
      <p>This is the paragraph of text that will be displayed when you click the button.</p>
      {/if}
    </div>

    <div class="fifth-section">
      <h1>
        Benefits
      </h1>
      <h2>
        Save You Money.
      </h2>
      <div class="paragraph">
      <p> Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor <br> invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et
        <br> accusam et justo duo dolores et ea rebum. </p>
      </div>
      <div class="second-three-buttons">
        <div class="triplog-button">
          <button on:click={show3}></button>
          <span>Trip Log</span>
        </div>
        <div class="savedlocation-button">
          <button on:click={show3}></button>
          <span>Saved Location</span>
        </div>
        <div class="insurancelicense-button">
          <button on:click={show3}></button>
          <span>Vehicle Insurance & <br> Driver License</span>
        </div>
      </div>
      {#if shown3}
      <p>This is the paragraph of text that will be displayed when you click the button.</p>
      {/if}
    </div>
    
    <div id="scroll-target">
    <div class="sixth-section">
      <h1>
        On-demand Services
      </h1>
      <h2>
        Roadside Assistance.
      </h2>
      <div class="paragraph">
      <p> Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor <br> invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et </p>
      </div>
			<span class="roadsideImage">
				<picture>
					<source srcset={roadsideImage} type="image/png" class="container_img"/>
          <img src={welcome_fallback} alt="Welcome" />
				</picture>
			</span>
    </div>
  </div>

    <div class="seventh-section">
      <h1>
        On-demand Services
      </h1>
      <h2>
        Connect to Mechanics.
      </h2>
      <div class="paragraph">
      <p> Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor <br> invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et </p>
      </div>
      <span class="vehicleService">
				<picture>
					<source srcset={vehicleService} type="image/png" class="container_img"/>
          <img src={welcome_fallback} alt="Welcome" />
				</picture>
			</span>
    </div>

    <div class="eigth-section">
      <h1>
        On-demand Services
      </h1>
      <h2>
        Free Vehicle Health Report.
      </h2>
      <div class="paragraph">
      <p> Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor <br> invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et </p>
      </div>
      <span class="healthReport">
				<picture>
					<source srcset={healthReport} type="image/png" class="container_img"/>
          <img src={welcome_fallback} alt="Welcome" />
				</picture>
			</span>
    </div>
<div>
	<video
		poster="https://sveltejs.github.io/assets/caminandes-llamigos.jpg"
		src="https://sveltejs.github.io/assets/caminandes-llamigos.mp4"
		on:mousemove={handleMove}
		on:touchmove|preventDefault={handleMove}
		on:mousedown={handleMousedown}
		on:mouseup={handleMouseup}
		bind:currentTime={time}
		bind:duration
		bind:paused>
		<track kind="captions">
	</video>

	<div class="controls" style="opacity: {duration && showControls ? 1 : 0}">
		<progress value="{(time / duration) || 0}"/>

		<div class="info">
			<span class="time">{format(time)}</span>
			<span>click anywhere to {paused ? 'play' : 'pause'} / drag to seek</span>
			<span class="time">{format(duration)}</span>
		</div>
	</div>
</div>
    <div class="footer">
      <Footer/>
  </div>
</div>



<style>
  /* .carousel {
    position: relative;
    overflow: hidden;
    width: 600px;
    height: 400px;
  }
  .carousel-slides {
    display: flex;
    transition: transform 1s;
  }
  .carousel-slide {
    flex: 0 0 100%;
    width: 100%;
    height: 100%;
  }
  .carousel-slide img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  .carousel-controls {
    position: absolute;
    bottom: 20px;
    left: 0;
    right: 0;
    display: flex;
    justify-content: center;
  }
  .carousel-control {
    cursor: pointer;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    background-color: rgba(0, 0, 0, 0.5);
    color: #fff;
    text-align: center;
    line-height: 30px;
    margin: 0 10px;
  }
  .carousel-control:hover {
    background-color: rgba(0, 0, 0, 0.7);
  }
  .carousel-control.active {
    background-color: #000;
  } */
  
  li {
    display: block;
    line-height: 3;
    margin-bottom: 20em;
  }

.scroll-link {
    cursor: pointer;
  }
  .scroll-link:hover {
    text-decoration: underline;
  }

  div {
		position: relative;
	}

	.controls {
		position: absolute;
		top: 0;
		width: 100%;
		transition: opacity 1s;
	}

	.info {
		display: flex;
		width: 100%;
		justify-content: space-between;
	}


	.time {
		width: 3em;
	}

	.time:last-child { text-align: right }

	progress {
		display: block;
		width: 100%;
		height: 10px;
		-webkit-appearance: none;
		appearance: none;
	}

	progress::-webkit-progress-bar {
		background-color: rgba(0,0,0,0.2);
	}

	progress::-webkit-progress-value {
		background-color: rgba(255,255,255,0.6);
	}

	video {
		width: 100%;
	}
  .benefits-section {
    position: fixed;
    top: 10em;
    left: 1em;
  }

  .benefits-section button{
    position: absolute;
    text-align: center;
    width:100px;
    height:40px;
    border-radius: 30px;
    background: #F4D19B;
    border:#707070;
    color: #000000;
  }

  .benefits-section button:hover{
    background: #83B0D1;
    color: #475569;
  }

  h4{
    margin-bottom: -1em;
  }

  .healthReport img{
    position: relative;
    width: 12em;
    height: 20em;
    left: 28em;
    bottom: 3em;
  }

  .roadsideImage img{
    position: relative;
    width: 12em;
    height: 20em;
    left: 28em;
    bottom: 3em;
  }

  .vehicleService img{
    position: relative;
    width: 12em;
    height: 20em;
    left: 28em;
    bottom: 3em;
  }

  .roadside-button button{
        background-image: url('./tow-truck-svgrepo-com.png');
        background-repeat: no-repeat;
        background-position: center;
        margin-left: -3.9em;
        width: 67px;
        height: 68px;
        font-size: 2rem;
        background-size: 38.53px 19.73px;
        border-radius: 100px;
        border: #3D6889;
        background-color:#83B0D1;
    }
    
    .roadside-button span {
        position: relative;
        margin-right: 2em;
    }

    .healthservice-button button{
        background-image: url('./tool-svgrepo-com.png');
        background-repeat: no-repeat;
        background-position: center;
        width: 67px;
        height: 68px;
        margin-left: -3.6em;
        font-size: 2rem;
        background-size: 25.5px 26.17px;
        border-radius: 100px;
        border: #3D6889;
        background-color:#83B0D1;
    }

    .healthservice-button span {
      position: relative;
      margin-right: 2em;
    }

    .healthreport-button button{
        position: relative;
        background-image: url('./healthimage.png');
        background-repeat: no-repeat;
        background-position: center;
        width: 67px;
        height: 68px;
        font-size: 2rem;
        margin-left: -3.8em;
        background-size: 22.56px 37.6px;
        border-radius: 100px;
        border: #3D6889;
        background-color:#83B0D1;
    }

    .healthreport-button span {
        position: relative;
        margin-right: 2em;
    }

    .crashdetection-button button{
        position: relative;
        background-image: url('./car-crash-svgrepo-com (1).png');
        background-repeat: no-repeat;
        background-position: center;
        width: 67px;
        height: 68px;
        font-size: 2rem;
        margin-left: -4.4em;
        background-size: 22.56px 37.6px;
        border-radius: 100px;
        border: #3D6889;
        margin-right: 68.4px;
        background-color:#83B0D1
    }

    .crashdetection-button span {
        position: relative;
        margin-right: 2em;
    }

    .voiceassistant-button button{
        position: relative;
        background-image: url('./microphone-svgrepo-com.png');
        background-repeat: no-repeat;
        background-position: center;
        width: 67px;
        height: 68px;
        font-size: 2rem;
        margin-left: -4.6em;
        background-size: 22.56px 37.6px;
        border-radius: 100px;
        border: #3D6889;
        margin-right: 66.4px;
        background-color:#83B0D1;
    }


    .triplog-button button{
        position: relative;
        background-image: url('./triplog.png');
        background-repeat: no-repeat;
        background-position: center;
        width: 67px;
        height: 68px;
        font-size: 2rem;
        margin-left: -5.3em;
        background-size: 22.56px 37.6px;
        border-radius: 100px;
        border: #3D6889;
        background-color:#83B0D1;
    }

    .triplog-button span {
        position: relative;
        margin-right: 6em;
    }

    .savedlocation-button button{
        position: relative;
        background-image: url('./location.png');
        background-repeat: no-repeat;
        background-position: center;
        width: 67px;
        height: 68px;
        font-size: 2rem;
        margin-left: -4.6em;
        background-size: 22.56px 37.6px;
        border-radius: 100px;
        border: #3D6889;
        background-color:#83B0D1;
    }

    .savedlocation-button span {
        position: relative;
        margin-right: 6em;
    }

    .insurancelicense-button button{
        position: relative;
        background-image: url('insurancelicense.png');
        background-repeat: no-repeat;
        background-position: center;
        width: 67px;
        height: 68px;
        font-size: 2rem;
        margin-left: -4.4em;
        background-size: 22.56px 37.6px;
        border-radius: 100px;
        border: #3D6889;
        background-color:#83B0D1;
    }

    .coupons-button button{
        position: relative;
        background-image: url('./coupon-svgrepo-com.png');
        background-repeat: no-repeat;
        background-position: center;
        width: 67px;
        height: 68px;
        font-size: 2rem;
        margin-left: -5.25em;
        background-size: 22.56px 37.6px;
        border-radius: 100px;
        border: #3D6889;
        background-color:#83B0D1;
    }

    .coupons-button span {
        position: relative;
        margin-right: 6em;
    }

    .tools-button button{
        position: relative;
        background-image: url('./tools.png');
        background-repeat: no-repeat;
        background-position: center;
        width: 67px;
        height: 68px;
        font-size: 2rem;
        margin-left: -5.6em;
        background-size: 22.56px 37.6px;
        border-radius: 100px;
        border: #3D6889;
        margin-right: 68.4px;
        background-color:#83B0D1
    }

    .tools-button span {
        position: relative;
        margin-right: 5em;
    }

    .tco-button button{
        position: relative;
        background-image: url('./money-svgrepo-com (2).png');
        background-repeat: no-repeat;
        background-position: center;
        width: 67px;
        height: 68px;
        font-size: 2rem;
        margin-left: -3.8em;
        background-size: 22.56px 37.6px;
        border-radius: 100px;
        border: #3D6889;
        margin-right: 66.4px;
        background-color:#83B0D1;
    }

  .active {background-color: #F4D19B; color: #83B0D1;}
  button:hover {background-color: #F4D19B; color: #83B0D1;}

/* .scroll-progress-bar {
    position: fixed;
    top: 0;
    left: 0;
    width: 4px;
    height: 100%;
    background-color: #ddd;
  }

  .scroll-progress {
    width: 4px;
    height: 0;
    background-color: blue;
    transition: height 0.2s;
  } */

  span {
    position: relative;
    display: flex;
    top: 2em;
    right: 8.5em;
  }

  .second-section {
    position: relative;
    margin-top: 25rem;
    left: 50em;
  }

  .third-section {
    position: relative;
    margin-top: 30rem;
    left: 50em;
  }

  .fourth-section {
    position: relative;
    margin-top: 40rem;
    left: 50em;
  }

  .fifth-section {
    position: relative;
    margin-top: 40rem;
    left: 50em;
  }

  .sixth-section {
    position: relative;
    margin-top: 20rem;
    left: 50em;
  }

  .seventh-section {
    position: relative;
    margin-top: 20rem;
    left: 50em;
  }

  .eigth-section {
    position: relative;
    margin-top: 20rem;
    left: 50em;
  }

  .paragraph{
    position: relative;
    padding-top: 1rem;
    padding-bottom: 5rem;
  }

  .first-three-buttons{
    position: relative;
    display:inline-flex;
    margin-inline: 9em;
    padding-bottom: 5em;
  }

  .two-buttons{
    position: relative;
    display:inline-flex;
    margin-inline: 9em;
    padding-bottom: 5em;
  }

  .second-three-buttons{
    position: relative;
    display:inline-flex;
    margin-inline: 9em;
    padding-bottom: 5em;
  }

  .third-three-buttons{
    position: relative;
    display:inline-flex;
    margin-inline: 9em;
    padding-bottom: 5em;
  }

  .container {
      display: flex;
		  flex-direction: column;
		  min-height: 100vh;
      overflow-x: hidden;
    }

    .next-button {
      position: relative;
      right: 62em;
      top: 34em;
    }

    .prev-button {
      position: relative;
      top: 34em;
      left:6em;
    }
 
 .header{
    position: fixed;
    top:-1em;
    z-index: 1;
 }
.footer{
  position: relative;
  display: block;
  margin-top: -1em;
}
 h1 + h2 {
  line-height: 1px;
 }

 h4 + h5 {
  line-height: -1px;
 }

 h3 {
  position: relative;
  left: 17.5em;
  word-spacing: 18em;
 }

 .carousel {
      display: flex;
      position: flex;
      margin-left: 12em;
      margin-top: 6rem;
    }

    .carousel img {
      width: 150vh;
      height: 80vh;
      align-self: center;
    }
  
    .slide {
      transition: transform 0.5s ease;
      flex:1;
    }

      /* define the "enter" and "leave" states for the animation */
    .slide-caption {
      font-size: 18px;
      font-weight: bold;
      text-align: center;
      margin-left: 35rem;
    }

    .progress-bar {
    width: 25rem; /* set the initial width of the progress bar */
    height: 1rem;
    align-items: baseline;
    background-color: #868686;
    border-radius: 10px;
    margin-inline: 22rem;
    margin-top: -5rem;
  }


  .progress-bar-fill {
    height: 100%;
    background-color: #3D6889;
    border-radius: 10px;
    transition: width 0.5s; /* add a transition effect when the width changes */
  }

  /* .icon {
    width: 20px;
    height: 20px;
    background-color: #fff;
    border-radius: 50%;
    display: inline-block;
    text-align: center;
    line-height: 20px;
  } */



</style>


