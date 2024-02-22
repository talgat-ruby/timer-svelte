<script lang="ts">
  import {createEventDispatcher, onMount} from 'svelte';

  const dispatch = createEventDispatcher();

  let count: number = 0

  let timerId = 0

  export let id: string

  const stopCounter = () => {
    window.clearInterval(timerId);
  };

  const startCounter = () => {
    timerId = setInterval(() => {
      count = count + 1;
    }, 1000);
  };

  const handlePause = () => {
    stopCounter();
  };

  const handleStop = () => {
    stopCounter();
    count = 0;
  };

  const handleStart = () => {
    startCounter();
  };

  const handleDelete = () => {
    dispatch("delete", id)
  }

  onMount(() => {
    handleStart();

    return () => {
      console.log("component destroyed");
      stopCounter();
    }
  })
</script>

<div class="counter">
  <p>{count}</p>
  <button on:click={handlePause}>Pause</button>
  <button on:click={handleStop}>Stop</button>
  <button on:click={handleStart}>Start</button>
  <button on:click={handleDelete}>Delete</button>
</div>

<style>
  .counter {
    margin-inline-start: 2rem;
  }
</style>
