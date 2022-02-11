<script>
  import { addDoc, serverTimestamp } from 'firebase/firestore'
  export let colRef;
  export let user;
  
  // adds message to database
  let text = '';
  const handleSubmit = () => {
    addDoc(colRef, {
      uid: user.uid,
			message: text,
			avatar: user.photoURL,
      createdAt: serverTimestamp()
    })
    text = '';
    textbox.focus();
  }

  // submits if enter key pressed
  const handleEnter = (e) => {
    if (e.key === 'Enter') {
      handleSubmit();
    }
  }

	// for focus
	let textbox;

	// disabled button if no text
	let isEmpty = true;
	$: if (text != '') {
		isEmpty = false;
	}
	else {
		isEmpty = true;
	}
</script>

<div class="form">
  <div class="form__textbox">
    <input 
      class="form__input"
      type="text" 
      placeholder="Message" 
      bind:this={textbox}
      bind:value={text}
      on:keydown={handleEnter}
    />
    <span class="form__submit-button" class:inactive={isEmpty} on:click={handleSubmit}>
      <i class="fas fa-arrow-circle-up"></i>
    </span>
  </div>
</div>

<style>
  .form {
    padding: 5px 30px 30px;

  }

  .form__textbox {
    display: flex;
    align-items: center;
    flex-direction: row;
    border: 1px solid rgb(204, 204, 204);
    border-radius: 50px;
    padding-right: 9px;
    padding-bottom: 2px;
  }

  .form__input {
    flex-grow: 2;
    border: none;
    background: transparent;
    padding-left: 20px;
  }

  .form__input:focus {
    outline: none;
  }

  .form__submit-button {
    font-size: 30px;
    color: #1982FC;
    cursor: pointer;
  }

  .inactive, .inactive:hover {
    color: rgb(204, 204, 204);
    cursor: default;
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