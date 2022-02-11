<script>
	// imports/exports
	export let user;
	export let signout;
	import Header from './components/Header.svelte';
	import MessageHistory from './components/MessageHistory.svelte';
	import Message from './components/Message.svelte';
	import Form from './components/Form.svelte';
	import {
    getFirestore, collection, onSnapshot,
    addDoc, deleteDoc, doc,
    query, where,
    orderBy, serverTimestamp,
    getDoc, updateDoc
  } from 'firebase/firestore'

	let userCount = 0;

	// setup db
	const db = getFirestore();
	const colRef = collection(db, 'messages');
	const q = query(colRef, orderBy('createdAt'));  
	
	// subscribe to db
	let msgs = [];

	const unsub = onSnapshot(q, (querySnapshot) => { 
		let messages = [];
		querySnapshot.docs.forEach((doc) => {
      messages.push({ ...doc.data(), id: doc.id })
    })
		msgs = messages;

		// counting number of unique IDs
		let IDList = messages.map((x) => {
        return x.uid;
    });		

		const countUnique = (iterable) => {
			return new Set(iterable).size;
		}

		userCount = countUnique(IDList);
  });
	
</script>

<div class="chatroom">
	<Header {signout} {userCount}/>
	<MessageHistory>
		{#each msgs as msg}
			<Message {msg} {user}/>
		{/each}
	</MessageHistory>

	<Form {user} {colRef}/>

</div>

<style>
	.chatroom {
    max-height: 100vh;
    overflow: auto;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}
</style>