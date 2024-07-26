<script>
  let isMenuOpen = false;

  function toggleMenu() {
    isMenuOpen = !isMenuOpen;
  }
</script>

<header class="header">
  <div class="container">
    <div class="brand">
    <img src="/online-shop.png" alt="Flowbite Logo" />SwiftCart
    </div>
    <nav class="nav-links">
     <a href="/">Login</a>
      <a href="/">Cart</a>
      <a href="/">Wishlist</a>
    </nav>
    <button class="menu-button" on:click={toggleMenu}>
      <svg class="menu-icon" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7"></path>
      </svg>
    </button>
  </div>
  {#if isMenuOpen}
    <nav class="mobile-nav">
      <a href="/">Login</a>
      <a href="/">Cart</a>
      <a href="/">Wishlist</a>
    </nav>
  {/if}
</header>

<style>
  .header {
    background-color: grey;
    color: white;
    padding: 16px;
  }

  .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: 1200px;
    margin: 0 auto;
  }

  .brand {
    font-size: 24px;
    font-weight: bold;
  }

  .brand img {
    height: 32px;
  }

  .nav-links {
    display: none;
  }

  .nav-links a {
    margin-left: 16px;
    text-decoration: none;
    color: white;
  }

  .menu-button {
    background: none;
    border: none;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
  }

  .menu-icon {
    width: 24px;
    height: 24px;
    color: white;
  }

  .mobile-nav {
    display: flex;
    flex-direction: column;
    margin-top: 16px;
  }

  .mobile-nav a {
    text-decoration: none;
    color: white;
    padding: 8px 0;
  }

  @media (min-width: 768px) {
    .nav-links {
      display: flex;
    }

    .menu-button {
      display: none;
    }

    .mobile-nav {
      display: none;
    }
  }
</style>