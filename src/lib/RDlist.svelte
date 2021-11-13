<script>
	import { Router, Link, Route } from "svelte-routing";
 import {rd} from "../rd.json"
</script>
<center>
                        
           {#each rd as r}
        
     <div id="{r.category}">        
                  <img src="{r.image}" width="100" id="radio" />
             <br>
             <br>
     <Link to="/radio/{r.route}" class="link">Listen</Link>
                          <br>
             <br>
                </div>

               {/each}
                          
                  </center>
									<style>
										#radio {
        border-radius:100%;
}
#radio:hover {
        content: "Listen";
        transition: 1s;
}
									</style>