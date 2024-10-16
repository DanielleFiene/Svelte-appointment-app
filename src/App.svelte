<script>
	import ContactForm from './components/ContactForm.svelte';
  </script>

<main>
	<h1>Contact and Appointment Manager</h1>
	<ContactForm />
</main>

<style>
	main {
		padding: 1em;
		max-width: 600px;
		margin: 0 auto;
	}

	h1 {
		text-align: center;
		color: #cccccc;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 400;
		text-decoration: underline overline;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>