<script>
    export let appointments = []; // Pass appointments array as a prop

    // Function to delete an appointment
    function deleteAppointment(index) {
        // Remove the appointment at the specified index
        appointments.splice(index, 1);

        // Save the updated appointments array to local storage
        localStorage.setItem('appointments', JSON.stringify(appointments));

        // Trigger an update by creating a new reference to the array
        appointments = [...appointments]; // This ensures that Svelte reacts to the change
    }

    // Function to sort appointments by date and time
    function sortAppointments(appointments) {
        return appointments.sort((a, b) => {
            // Combine date and time into a single comparable Date object
            const dateTimeA = new Date(`${a.appointmentDate.split('/').reverse().join('-')}T${a.appointmentTime}`);
            const dateTimeB = new Date(`${b.appointmentDate.split('/').reverse().join('-')}T${b.appointmentTime}`);
            return dateTimeA - dateTimeB; // Ascending order
        });
    }
</script>

<!-- Appointment List -->
<div class="appointment-list">
    <h2><span class="highlight">Upcomin</span><span class="highlight2">g Appointments</span></h2>
    {#if appointments.length === 0}
        <p>No appointments yet.</p>
    {:else}
        <ul>
            {#each sortAppointments(appointments) as appointment, index}
                <li>
                    <strong class="appointment-name">{appointment.appointmentName}</strong>
                    <div class="appointment-details">
                        <div class="appointment-info">
                            <strong>Date: </strong>{appointment.appointmentDate}<br />
                            <strong>Time: </strong>{appointment.appointmentTime}<br />
                            <strong>Contact: </strong>{appointment.contact}
                        </div>
                    </div>
                    <button on:click={() => deleteAppointment(index)}>Delete</button>
                </li>
            {/each}
        </ul>
    {/if}
</div>

<style>
/* Appointment List Styles */
.appointment-list {
    max-width: 80%;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
}

.appointment-list p {
    text-align: center;
    color: #F0F0F0;
}

.appointment-list h2 {
    margin-bottom: 20px;
    font-weight: 600;
    font-size: 1.5rem;
    text-decoration: underline overline;
    text-align: center;
}

.highlight {
    color: #333333;
}

.highlight2 {
    color: #F0F0F0;
}

/* Flex container for list items */
ul {
    list-style: none;
    padding: 0;
}

li {
    display: flex;
    align-items: center; /* Center items vertically */
    justify-content: space-between; /* Space between left and right items */
    background-color: #ffffff;
    border-radius: 8px;
    padding: 15px;
    margin-bottom: 10px;
    box-shadow: 0 10px 40px 20px rgba(0, 0, 0, 0.6);
    font-weight: 500;
}

/* Style for the appointment name */
.appointment-name, .appointment-details {
    flex: 1; /* Take up equal width */
    text-align: left; /* Align content to the left */
    margin-right: 10px;
}

/* Adjust the width of the appointment name */
.appointment-name {
    overflow-wrap: break-word;
    max-width: 180px;
    margin-right: 50px;
}

/* Flex container for the appointment details */
.appointment-details {
    display: flex;
    justify-content: flex-start; /* Align content to the left */
    align-items: center;
    height: 150px;
}

/* Align appointment info vertically */
.appointment-info {
    text-align: left;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
}

/* Button to delete appointments */
li button {
    background-color: #e74c3c;
    color: white;
    border: none;
    padding: 10px 15px;
    border-radius: 8px;
    font-size: 0.9rem;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.1s ease;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
    flex: 0;
}

/* Hover effect for the delete button */
li button:hover {
    background-color: #c0392b;
}

/* Active button effect */
li button:active {
    transform: scale(0.95);
    background-color: #732219;
    box-shadow: none;
}

</style>
