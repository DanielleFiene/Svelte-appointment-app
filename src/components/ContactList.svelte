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
    <h2>Contact List</h2>
    {#if contacts.length === 0}
      <p>No contacts yet.</p>
    {:else}
      <ul>
        {#each contacts as contact, index}
          <li>
            {contact.name} <br />
            Phone: {contact.phone} <br />
            Email: {contact.email}
            <button on:click={() => deleteContact(index)}>Delete</button>
          </li>
        {/each}
      </ul>
    {/if}
</div>

<style>
    /* Contact List Styles */
    .contact-list {
      max-width: 40%;
      margin: 0 auto;
      display: flex;
      flex-direction: column;
    }
  
    .contact-list h2 {
      margin-bottom: 20px;
      font-weight: 600;
      font-size: 1.5rem;
      text-decoration: underline overline;
      color: #cccccc;
      text-align: center;
    }

    .contact-list p {
        color: #cccccc;
    }
  
    ul {
      list-style: none;
      padding: 0;
    }
  
    li {
      display: flex;
      justify-content: space-between;
      align-items: center; 
      background-color: #ffffff;
      border-radius: 8px;
      padding: 15px;
      margin-bottom: 10px;
      box-shadow: 0 20px 40px 20px rgba(0, 0, 0, 0.6);
      font-weight: 500;
    }
  
    /* Button to delete contacts */
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
