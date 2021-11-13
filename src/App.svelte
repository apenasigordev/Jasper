<script>
  import logo from './assets/svelte.png'
  import RDlist from './lib/RDlist.svelte'
        import { Router, Link, Route } from "svelte-routing";
        export let url = "";
        import { fade,fly } from 'svelte/transition';
        import {rd} from "./rd.json"
        import Icon from 'mdi-svelte';
        import { mdiArrowLeft } from '@mdi/js';
        import axios from "axios";
        import { onMount } from 'svelte';

  let ready = false;
  onMount(() => ready = true);
        export let icon = mdiArrowLeft
        let characterName;
        export let current="";
        export let params;
        let time;
        let duration;
	      let paused;
let p;
        //export let location = window.locatonon
        function format(seconds) {
		if (isNaN(seconds)) return '...';

		const minutes = Math.floor(seconds / 60);
		seconds = Math.floor(seconds % 60);
		if (seconds < 10) seconds = '0' + seconds;

		return `${minutes}:${seconds}`;
        }
	function play() {
		p.play()
	}
           </script>

<Router url="{url}" >
      
					 
    <div transition:fly={{ y: -200, delay: 550, duration: 500}}>
               <RDlist/>
		</div>
        
         <Route path="/radio/:id" let:params>
					 
<center>
					 <div style="z-index:-1; position: fixed; bottom:0;" in:fly={{ x:-400, y:0, delay: 1500, duration: 1000}} out:fly={{ x: 400, y:0, delay: 100, duration: 300 }}>
                 {#each rd as r}
                {#if params.id === r.route}
                 
                  <center>
                         <audio
	autoplay
poster="{r.image}"
	src="{r.listen}"
        bind:currentTime={time}
         bind:paused={paused}                                                                                
  bind:duration={duration}
					bind:this={p}																																				 
        class="audio-player">                                                                >
	<track kind="captions">
</audio>
                <div class="audio-player">
  <div class="timeline">
    <!--<input type="range" style="background:pink;" class="progress" min="0" max="100" value="{time}"/>-->
  </div>
  <div class="controls">
    <div class="play-container">
            {#if paused}
			<button style="background: transparent; border:none;" on:click={p.play()}>
      <div class="toggle-play play">
    </div>
			</button>
			{:else}
			<button style="background: transparent; border:none;" on:click={p.pause()}>
      <div class="toggle-play pause">
    </div>
</button>
			{/if}
    </div>
    <div class="time">
      <div class="current">{format(time)}</div>
      <div class="divider">/</div>
      <div class="length">{duration}</div>
    </div>
    <div class="name">{r.name}</div>
<!--     credit for icon to https://saeedalipoor.github.io/icono/ -->
   
      </div>
</div>
									</center>
                 {/if}
         {/each}
</div>
</center>
         </Route>
</Router>
  <style>
  :root {
     padding:0;margin:0;  
    background:#4E2D46;
          color:white;
          font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
      Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }
#radio {
        border-radius:100%;
}
#radio:hover {
        content: "Listen";
        transition: all 1s;
}
		
          #home {
                  width:100%;
                  height: 50%;
          }
		
          .audio-player {
  height: 50px;
  width:420px;
  background: purple;
  box-shadow: 0 0 20px 0 #000a;
  font-family: arial;
  color: white;
  font-size: 0.75em;
  overflow: hidden;
  display: grid;
  grid-template-rows: 6px auto;
						border-radius:20px;
						bottom:0;
						position: fixed;
					/*	z-index:-1;*/
						transition: all 0.5s;
}
          .audio-player .timeline {
  background: white;
  width: 100%;
  position: relative;
  cursor: pointer;
  box-shadow: 0 2px 10px 0 #0008;
}
.audio-player .timeline .progress {
  background: deeppink;
  width: 0%;
  height: 100%;
  transition: 0.25s;
}
.audio-player .controls {
  display: flex;
  justify-content: space-between;
  align-items: stretch;
  padding: 0 20px;
}
.audio-player .controls > * {
  display: flex;
  justify-content: center;
  align-items: center;
}
.audio-player .controls .toggle-play.play {
  cursor: pointer;
  position: relative;
  left: 0;
  height: 0;
  width: 0;
  border: 7px solid #0000;
  border-left: 13px solid deeppink;
	transition: all 0.5s;
}
.audio-player .controls .toggle-play.play:hover {
  transform: scale(1.1);
}
.audio-player .controls .toggle-play.pause {
  height: 15px;
  width: 20px;
  cursor: pointer;
  position: relative;
}
.audio-player .controls .toggle-play.pause:before {
  position: absolute;
  top: 0;
  left: 0px;
  background: deeppink;
  content: "";
  height: 15px;
  width: 3px;
	transition: all 0.5s;
}
.audio-player .controls .toggle-play.pause:after {
  position: absolute;
  top: 0;
  right: 8px;
  background: deeppink;
  content: "";
  height: 15px;
  width: 3px;
	transition: all 0.5s;
}
.audio-player .controls .toggle-play.pause:hover {
  transform: scale(1.1);
}
          .audio-player .controls .time {
  display: flex;
}
.audio-player .controls .time > * {
  padding: 2px;
                }
          .audio-player .controls .volume-container {
  cursor: pointer;
  position: relative;
  z-index: 2;
}
.audio-player .controls .volume-container .volume-button {
  height: 26px;
  display: flex;
  align-items: center;
}
.audio-player .controls .volume-container .volume-button .volume {
  transform: scale(0.7);
          }
          .link > :global(a) {
        text-decoration: none;
                  /*color:white;
                  background: deeppink;
                  border: 10px solid deeppink;
                  border-radius: 15px;*/
    }
          :global(a) {
        text-decoration:none;
        color:white;
                  background: deeppink;
                  border: 10px solid deeppink;
                  border-radius: 10px;          
}
</style>
