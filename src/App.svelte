<script>
	import Chatroom from './Chatroom.svelte';

	// firebase imports
	import { firebaseConfig } from './firebaseConfig'
  import { initializeApp } from 'firebase/app';
	import { 
		getAuth, 
		signInWithPopup, GoogleAuthProvider, 
		signOut, onAuthStateChanged 
	} from "firebase/auth";

  // firebase auth
	initializeApp(firebaseConfig);
	const provider = new GoogleAuthProvider();
	const auth = getAuth();
	let user;

	const login = () => {
		signInWithPopup(auth, provider)
	}

	const signout = () => {
		signOut(auth)
	}

	onAuthStateChanged(auth, (usr) => {
		user = usr;
  });
</script>

<main>
	{#if user}
		<Chatroom {user} {signout}/> 
	{:else}
		<div class="login-form">
			<button on:click={login}>
				<i class="fa fa-google"></i>
				Sign In with Google
			</button>
		</div>
	{/if}
</main>

<style>
	.login-form {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%,-50%);	
	}
	.login-form button {
		padding: 10px;
		background: #fff;
		color: #111;
		font-size: 16px;
		cursor: pointer;
		outline: none;
		border: 1px solid #bbb;
	}
	.login-form button i.fa {
		padding-right: 10px;
		border-right: 1px solid #ddd;
		color: #555;
	}
</style>