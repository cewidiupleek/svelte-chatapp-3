<script>
  export let signout;
</script>


<header>
  <h3>Cool Kids GC</h3>
  <div class="member-count">
    <i class="fas fa-user-friends"></i>
    <p>3</p>
  <button on:click={signout}>Log out</button>
</header>


<style>

  header {
    box-shadow: 0px -8px 17px 14px #cbcbcb;
    height: 80px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  h3 {
    margin-right: 30px;
  }

  .member-count {
    display: flex;
    align-items: center;
    gap: 5px;
    color: grey;
  }

  button {
    margin-left: 30px;
    border-radius: 50px;
    color: white;
    background-color: #1982FC;
    border: 2px solid #1982FC;
    cursor: pointer;
    padding: 5px 5px;
    transition: 0.3s;

  }

  button:hover {
    color: #1982FC;
    background-color: white;
    border: 2px solid #1982FC;
  }
</style>
