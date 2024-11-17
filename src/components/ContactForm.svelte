<script>
    import ContactList from './ContactList.svelte'; // Import the ContactList component
    let name = "";
    let phone = "";
    let email = "";
    let selectedCountryCode = "+31"; // Default value, e.g., Holland
    let contacts = []; // Hold contacts locally and pass them as a prop

    // Country codes array
    const countryCodes = [
        { code: "+1", name: "United States" },
        { code: "+44", name: "United Kingdom" },
        { code: "+31", name: "The Netherlands" },
        { code: "+49", name: "Germany" },
        { code: "+33", name: "France" },
        { code: "+39", name: "Italy" },
        { code: "+34", name: "Spain" },
        { code: "+420", name: "Czech Republic" },
    ];

    // Load contacts from localStorage when component mounts
    function loadContacts() {
        const storedContacts = localStorage.getItem('contacts');
        contacts = storedContacts ? JSON.parse(storedContacts) : [];
    }

    // Function to add a new contact
    function addContact() {
        const newContact = {
            name,
            phone: `${selectedCountryCode} ${phone}`,
            email
        };

        // Load contacts from local storage
        const storedContacts = localStorage.getItem('contacts');
        const currentContacts = storedContacts ? JSON.parse(storedContacts) : [];

        // Add new contact to contacts array and save it
        currentContacts.push(newContact);
        localStorage.setItem('contacts', JSON.stringify(currentContacts));

        // Update local contacts array immediately
        contacts = [...currentContacts];

        // Clear form fields
        name = "";
        phone = "";
        email = "";
        selectedCountryCode = countryCodes[2].code; // Resetting the country code to default +31
    }

    // Load the contacts when the component initializes
    loadContacts();
</script>

<!-- Contact Form -->
<div class="contact-form">
    <h2>Add New Contact</h2>
    <form on:submit|preventDefault={addContact}>
        <label for="name">Name:</label>
        <input id="name" type="text" bind:value={name} placeholder="Contact Name" required />

        <label for="countryCode">Country Code:</label>
        <select id="countryCode" bind:value={selectedCountryCode} required>
            {#each countryCodes as { code, name }}
                <option value={code}>{name} ({code})</option>
            {/each}
        </select>

        <label for="phone">Phone Number:</label>
        <input id="phone" type="tel" bind:value={phone} placeholder="Your number without country code" required title="Please enter a valid phone number without the country code." />

        <label for="email">Email Address:</label>
        <input id="email" type="email" bind:value={email} placeholder="contact@example.com" required pattern="^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,50}$" title="Please enter a valid email address, e.g., contact@example.com."/>
        
        <!-- Wrapper for centering the button -->
        <div class="button-wrapper">
            <button type="submit">Add Contact</button>
        </div>
    </form>
</div>

<!-- Pass the contacts array to ContactList component -->
<ContactList {contacts} />

<style>
    /* Basic styles for form */
    .contact-form {
        background-color: #ffffff;
        border-radius: 12px;
        padding: 20px;
        margin: 0 auto;
        width: 70%;
        box-shadow: 0 0 40px 20px rgba(0, 0, 0, 0.6);
        margin-bottom: 40px;
    }

    .contact-form h2 {
        margin-bottom: 20px;
        font-weight: 600;
        font-size: 1.5rem;
        color: #2c3e50;
        margin: 0 auto;
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

    /* Add contact button style */
    button {
        width: 30%;
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

    @media (min-width: 500px) and (max-width: 999px) {
        .contact-form {
            width: 100%;
            margin: 0 auto;
            display: flex;
            flex-direction: column;
        }
    }
</style>
