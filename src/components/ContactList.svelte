<script>
    export let contacts = []; // Receive contacts array as a prop

    // Function to delete a contact
    function deleteContact(index) {
        // Remove the contact at the specified index
        contacts.splice(index, 1);

        // Save the updated contacts array to local storage
        localStorage.setItem('contacts', JSON.stringify(contacts));

        // Trigger an update by creating a new reference to the array
        contacts = [...contacts]; // This ensures that Svelte reacts to the change
    }
</script>

<!-- Contact List -->
<div class="contact-list">
    <h2><span class="highlight">Cont</span><span class="highlight2">act List</span></h2>
    {#if contacts.length === 0}
      <p>No contacts yet.</p>
    {:else}
      <ul>
        {#each contacts as contact, index}
            <li>
                <strong class="contact-name">{contact.name}</strong>
                <div class="contact-details">
                    <div class="contact-info">
                        <strong>Phone: </strong>{contact.phone}<br />
                        <strong>Email: </strong>{contact.email}
                    </div>
                </div>
                <button on:click={() => deleteContact(index)}>Delete</button>
            </li>
        {/each}
      </ul>
    {/if}
</div>

<style>
/* Contact List Styles */
.contact-list {
    max-width: 80%;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
}

.contact-list h2 {
    margin-bottom: 20px;
    font-weight: 600;
    font-size: 1.5rem;
    text-decoration: underline overline;
    text-align: center;
}

.contact-list p {
    text-align: center;
}

.highlight {
    color: #333333; /* Set color for the first 10 letters */
}

.highlight2 { /* Set color for the last letters */
	color: #F0F0F0; 
}

ul {
    list-style: none;
    padding: 0;
}

li {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background-color: #ffffff;
    border-radius: 8px;
    padding: 15px;
    margin-bottom: 10px;
    box-shadow: 0 10px 40px 20px rgba(0, 0, 0, 0.6);
    font-weight: 500;
}

.contact-name, .contact-details {
    flex: 1; /* Name and details take equal width */
    text-align: left; /* Align content to the left */
    margin-right: 10px; /* Add some space between details and button */
}

/* Adjust the width of the contact name */
.contact-name {
    overflow-wrap: break-word;
    max-width: 180px;
    margin-right: 50px;
}

/* Flex container for the contact details */
.contact-details {
    display: flex;
    justify-content: flex-start; /* Align content to the left */
    align-items: center;
    height: 100px;
}

.contact-info {
    display: flex;
    flex-direction: column;
    align-items: flex-start; /* Align contact info text to the left */
}

/* Button stays on the right */
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
    flex: 0; /* Prevent the button from stretching */
}

/* Hover effect */
li button:hover {
    background-color: #c0392b;
}

/* Active effect for button press */
li button:active {
    transform: scale(0.95);
    background-color: #732219;
    box-shadow: none;
}

</style>
