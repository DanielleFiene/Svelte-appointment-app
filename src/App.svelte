<script>
    import { Router, Route } from 'svelte-routing';
    import Sidebar from './components/Sidebar.svelte';
    import ContactForm from './components/ContactForm.svelte';
    import AppointmentCalendar from './components/AppointmentCalendar.svelte';
</script>

<main>
    <h1><span class="highlight">Contact an</span><span class="highlight2">d Appointment Manager</span></h1>

    <Router>
        <Sidebar /> <!-- Include the Sidebar inside the Router -->
        <div class="content"> <!-- Add a wrapper for the content -->
            <!-- Route for ContactForm, which is the default page -->
            <Route path="/" component={ContactForm} />
            <!-- Route for Appointment Calendar -->
            <Route path="/appointments" component={AppointmentCalendar} />
        </div>
    </Router>
</main>

<style>
    main {
        display: flex;
        justify-content: center;
		flex-direction: column;
        padding: 1em;
        max-width: 1500px; 
        margin: 0 auto;
    }

	h1 {
    position: relative;
    margin-left: 150px;
    display: flex;
    justify-content: center;
    text-align: center;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 400;
    margin-top: 20px;
    width: 100%;
	text-decoration: underline overline;
    flex-wrap: wrap;
}



.highlight {
    color: #333333; /* Set color for the first 10 letters */
    display: inline-block;
}

.highlight2 { /* Set color for the last letters */
	color: #F0F0F0; 
    display: inline-block;
}

    .content {
        margin-left: 220px; /* Add space for the sidebar */
        flex: 1; /* Allow content to grow */
    }
</style>
