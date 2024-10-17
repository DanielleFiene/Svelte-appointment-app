<!-- Sidebar.svelte -->
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
        height: 100vh; /* Full height */
        width: 200px; /* Fixed width for sidebar */
        position: fixed; /* Keep sidebar fixed */
        top: 0;
        left: 0;
    }

    .sidebar nav {
    display: flex;          /* Enable flexbox for the nav */
    flex-direction: column; /* Stack links vertically */
    justify-content: space-around; /* Center links horizontally */
    flex-grow: 1;           /* Make the nav take full width */
}

</style>
