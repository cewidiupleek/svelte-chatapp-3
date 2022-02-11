<script>
	import { beforeUpdate, afterUpdate } from 'svelte';

  let div;
  let autoscroll;

  beforeUpdate(() => {
    autoscroll = div && (div.offsetHeight + div.scrollTop) > (div.scrollHeight - 20);
  });

  afterUpdate(() => {
    if (autoscroll) div.scrollTo(0, div.scrollHeight);
  });


</script>

<div class="container" bind:this={div}>
  <slot></slot>
</div>

<style>
  .container {
    display: flex;
    flex-direction: column;
    flex-grow: 1; 
    gap: 3px;
    padding: 0px 30px;
		overflow: auto;
    position: relative;
    z-index: 1;
    background: transparent;

  }

  

  /* ------ scrolling ------ */
  ::-webkit-scrollbar {
    width: 17px;
  }

  /* Background */
  ::-webkit-scrollbar-track {
    background: transparent;
  }

  /* Handle */
  ::-webkit-scrollbar-thumb {
    background: rgb(155, 155, 155);
    border-radius: 50px; 
    background-clip: padding-box;
    padding: 0 4px;
    border-right: 5px solid transparent;
    border-left: 5px solid transparent;
  }

</style>