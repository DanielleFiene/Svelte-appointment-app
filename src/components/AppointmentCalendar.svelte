<script>
    import AppointmentList from './AppointmentList.svelte'; // Import the AppointmentList component
    import { onMount } from 'svelte'; // Import onMount lifecycle hook

    let appointmentName = "";
    let appointmentDate = ""; // Appointment date
    let appointmentTime = ""; // Appointment time
    let selectedContact = ""; // Placeholder for selected contact
    let appointments = []; // Hold appointments locally and pass them as a prop
    let contacts = []; // Array to hold contacts for selection

    // Load contacts from localStorage when the component mounts
    function loadContacts() {
        const storedContacts = localStorage.getItem('contacts');
        contacts = storedContacts ? JSON.parse(storedContacts) : [];
    }

    // Load appointments from localStorage
    function loadAppointments() {
        const storedAppointments = localStorage.getItem('appointments');
        appointments = storedAppointments ? JSON.parse(storedAppointments) : [];
    }

    // Function to add a new appointment
    function addAppointment() {
        const newAppointment = {
            appointmentName,
            appointmentDate,
            appointmentTime,
            contact: selectedContact // Include selected contact
        };

        // Load appointments from local storage
        const storedAppointments = localStorage.getItem('appointments');
        const currentAppointments = storedAppointments ? JSON.parse(storedAppointments) : [];

        // Add new appointment to appointments array and save it
        currentAppointments.push(newAppointment);
        localStorage.setItem('appointments', JSON.stringify(currentAppointments));

        // Update local appointments array immediately
        appointments = [...currentAppointments];

        // Clear form fields
        appointmentName = "";
        appointmentDate = "";
        appointmentTime = "";
        selectedContact = ""; // Resetting the selected contact
    }

    // Load the contacts and appointments when the component initializes
    onMount(() => {
        loadContacts();
        loadAppointments();
    });
</script>

<!-- Appointment Form -->
<div class="appointment-form">
    <h2>Add New Appointment</h2>
    <form on:submit|preventDefault={addAppointment}>
        <label for="appointmentName">Appointment Name:</label>
        <input id="appointmentName" type="text" bind:value={appointmentName} placeholder="Appointment Name" required />

        <label for="appointmentDate">Appointment Date (DD/MM/YYYY):</label>
        <input id="appointmentDate" type="text" bind:value={appointmentDate} placeholder="DD/MM/YYYY" required />

        <label for="appointmentTime">Appointment Time (24h format):</label>
        <input id="appointmentTime" type="time" bind:value={appointmentTime} required />

        <label for="contact">Select Contact:</label>
        <select id="contact" bind:value={selectedContact} required>
            <option value="" disabled>Select a contact</option>
            {#each contacts as contact}
                <option value={contact.name}>{contact.name}</option>
            {/each}
        </select>

        <div class="button-wrapper">
            <button type="submit">Add Appointment</button>
        </div>
    </form>
</div>

<!-- Pass the appointments array to AppointmentList component -->
<AppointmentList {appointments} />

<style>
    /* Basic styles for form */
    .appointment-form {
        background-color: #ffffff;
        border-radius: 12px;
        padding: 20px;
        margin: 0 auto;
        max-width: 70%;
        box-shadow: 0 0 40px 20px rgba(0, 0, 0, 0.6);
        margin-bottom: 40px;
    }

    .appointment-form h2 {
        margin-bottom: 20px;
        font-weight: 600;
        font-size: 1.5rem;
        color: #2c3e50;
    }

    label {
        margin: 0 0 5px 5px;
        font-weight: 500;
    }

    /* Style for input fields */
    input, select {
        display: block;
        width: 100%;
        padding: 12px;
        margin-bottom: 15px;
        border-radius: 8px;
        border: 1px solid #ddd;
        background-color: #fafafa;
        font-size: 1rem;
        transition: border-color 0.3s ease;
    }

    input:focus, select:focus {
        border-color: #3498db;
        outline: none;
    }

    /* Button wrapper to center the button */
    .button-wrapper {
        display: flex;
        justify-content: center;
    }

    /* Add appointment button style */
    button {
        width: 80%;
        background-color: #3498db; 
        color: white; 
        border: none;
        padding: 10px 15px;
        border-radius: 8px; 
        font-size: 1rem; 
        cursor: pointer; 
        transition: background-color 0.3s ease, transform 0.1s ease, box-shadow 0.3s ease;
        box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2); 
    }

    /* Hover effect */
    button:hover {
        background-color: #2980b9; 
        box-shadow: 0 6px 16px rgba(52, 152, 219, 0.4); 
    }

    /* Active effect for button press */
    button:active {
        transform: scale(0.95); 
        background-color: #1f639b; 
        box-shadow: none;
    }
</style>
