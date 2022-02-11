<script>
  export let user;
  export let msg;
  let time;
  $: show = false;

  const onMouseOver = () => {
    show = true;
    time = msg.createdAt.toDate().toLocaleTimeString([], {hour: 'numeric', minute:'2-digit'})
  }
  const onMouseOut = () => {
    show = false;
  }
</script>

{#if user.uid == msg.uid}
<!-- svelte-ignore a11y-mouse-events-have-key-events -->
  <div class="container-my-message">
    {#if show}
      <div class="time-right">
        <p>{time}</p>
      </div>
    {/if}
    <div class="bubble-my-message"
      on:mouseover={onMouseOver} 
      on:mouseout={onMouseOut} 
    >
      <div class="text-my-message">
        <p>{msg.message}</p>
      </div>
    </div>
  </div>
{:else}
  <div class="container-other-message">
    <!-- svelte-ignore a11y-mouse-events-have-key-events -->
    <div class="avatar"
      on:mouseover={onMouseOver} 
      on:mouseout={onMouseOut} 
    > 
      <img src={msg.avatar} alt="icon">
    </div>
    <!-- svelte-ignore a11y-mouse-events-have-key-events -->
    <div class="bubble-other-message"
      on:mouseover={onMouseOver} 
      on:mouseout={onMouseOut} 
    >
      <div class="text-other-message">
        <p>{msg.message}</p>
      </div>
    </div>
    {#if show}
      <div class="time-left">
        <p>{time}</p>
      </div>
    {/if}
  </div>
{/if}

<style>
    .container-my-message {
    display: flex;
    justify-content: flex-end;
  }

  .container-other-message {
    display: flex;
    justify-content: flex-start;
  }

  .bubble-my-message {
    display: flex;
    align-items: center;
    background-color: #1982FC;
    border-radius: 25px;
    padding: 0px 25px;
    max-width: 40vw;
  }

  .bubble-other-message {
    display: flex;
    align-items: center;
    background-color: #e9e9eb;
    border-radius: 25px;
    padding: 0 30px;
    max-width: 40vw;
  }

  .text-my-message {
    color: white;
    word-break: break-word;

  }

  .text-other-message {
    color: black;
    word-break: break-word;
  }

  .time-right {
    margin: auto 15px auto 0;
    font-size: 14px;
    color: rgb(104, 104, 104);
  }

  .time-left {
    align-items: center;
    margin: auto 0 auto 15px;
    font-size: 14px;
    color: rgb(104, 104, 104);
  }

  img {
    max-height: 53px;
    margin-right: 5px;
    clip-path: circle();
  }
</style>