<script>
    import { Router, Route, Link } from 'svelte-routing';
    import Sidebar from './components/Sidebar.svelte';
    import ContactForm from './components/ContactForm.svelte';
    import AppointmentCalendar from './components/AppointmentCalendar.svelte';
</script>

<main>
    <h1>
        <span class="highlight1">Contact</span>&nbsp;
        <span class="highlight2">and</span>&nbsp;
        <span class="highlight3">Appointment</span>&nbsp;
        <span class="highlight4">Manager</span>
    </h1>

    <Router>
        <div class="navigation">
            <!-- This will show only on smaller screens (below 1000px) -->
            <nav class="mobile-nav">
                <Link to="/" class="nav-link">Contacts</Link>
                <Link to="/appointments" class="nav-link">Appointments</Link>
            </nav>
        </div>

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
        text-align: center;
        text-transform: uppercase;
        font-size: 4em;
        font-weight: 600;
        margin-top: 20px;
        text-decoration: underline overline;
        text-decoration-color: #333;
    }

    h1 span {
        display: inline;
    }

    .highlight1 {
        color: #333333;
    }

    .highlight2 {
        color: #F0F0F0;
    }

    .highlight3 {
        color: #F0F0F0;
    }

    .highlight4 {
        color: #F0F0F0;
    }

    .content {
        margin-left: 220px; /* Add space for the sidebar */
        flex: 1;
    }

    /* Navigation Links (visible on small screens) */
    .mobile-nav {
        display: none; /* Hide by default */
        margin-top: 20px;
        text-align: center;
    }

    /* Media Queries for responsiveness */
    @media (max-width: 999px) {
        .sidebar {
            display: none; /* Hide sidebar */
        }

        /* Show mobile navigation */
        .mobile-nav {
            display: block; /* Show on smaller screens */
            margin-bottom: 20px;
        }

        .content {
            margin-left: 0; /* Remove margin for content when sidebar is hidden */
        }
    }

    @media (min-width: 1401px) and (max-width: 1900px) {
        h1 {
            font-size: 2em;
            margin-left: 25%;
        }
    }

    @media (min-width: 1000px) and (max-width: 1400px) {
        h1 {
            font-size: 1.5em;
            margin-left: 25%;
        }
    }

    @media (min-width: 740px) and (max-width: 999px) {
        h1 {
            font-size: 1.5em;
            margin: auto;
        }

        .content {
            display: flex;
            flex-direction: column;
            margin: auto;
        }
    }

    @media (min-width: 500px) and (max-width: 739px) {
        h1 {
            font-size: 1.2em;
        }
    }

    @media (min-width: 320px) and (max-width: 499px) {
        h1 {
            font-size: 1em;
        }
    }
</style>
