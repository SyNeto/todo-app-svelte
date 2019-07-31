<script>
	import { auth, googleProvider } from './firebase';
	import { authState } from 'rxfire/auth';

	import Profile from './Profile.svelte';

	let user;

	const unsubscribe = authState(auth).subscribe(u => user = u);
	const login = () => auth.signInWithPopup(googleProvider);
</script>


<section>
	{#if user}
		<Profile {...user} />
		<button on:click={ () => auth.signOut() }>Logout</button>
	{:else}
		<button on:click={login}>Signin with Google</button>
	{/if}
</section>
