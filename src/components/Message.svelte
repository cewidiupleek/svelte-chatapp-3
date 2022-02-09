<script>
  export let user;
  export let msg;
</script>

{#if user.uid == msg.uid}
  <div class="container-my-message">
    <div class="bubble-my-message">
      <p class="text-my-message">  
        {msg.message}
      </p>
    </div>
  </div>
{:else}
  <div class="container-other-message">
    <div class="avatar"> 
      <img src={msg.avatar} alt="icon">
    </div>
    <div class="bubble-other-message">
      <p class="text-other-message">  
        {msg.message}
      </p>
    </div>
  </div>
{/if}

<style>
  .container-my-message {
    display: flex;
    justify-content: flex-end;
    max-height: 40px;
  }

  .container-other-message {
    display: flex;
    justify-content: flex-start;
    max-height: 40px;
  }

  .bubble-my-message {
    display: flex;
    align-items: center;
    padding: 0 20px;
    background-color: #1982FC;
    border-radius: 50px;
    max-width: 500px;
  }

  .bubble-other-message {
    display: flex;
    align-items: center;
    background-color: #e9e9eb;
    border-radius: 50px;
    padding: 0px 20px;
    max-width: 500px;
  }

  .text-my-message {
    color: white;
  }

  .text-other-message {
    color: black;
  }

  img {
    height: 100%;
    margin-right: -40px;
    clip-path: circle();
  }

</style>