<script>
    import { Link } from 'svelte-routing';
</script>

<aside class="sidebar">
    <nav>
        <Link to="/">Contacts</Link>
        <Link to="/appointments">Appointments</Link>
    </nav>
</aside>

<style>
    .sidebar {
        display: flex;
        box-shadow: 10px 0 40px 20px rgba(0, 0, 0, 0.3);
        background-color: #f8f9fa;
        padding: 20px;
        border-right: 1px solid #ddd;
        height: 100vh; 
        width: 250px; 
        position: fixed;
        top: 0;
        left: 0;
    }

    .sidebar nav {
        display: flex;
        flex-direction: column; 
        justify-content: space-around; 
        flex-grow: 1;
    }

    /* Hide the sidebar on small screens */
    @media (max-width: 999px) {
        .sidebar {
            display: none; /* Hide sidebar */
        }
    }
</style>
