

<script>
    import './stylesheet.css';
</script>
<header title="My App" class="header">
    <nav>
      <a href="/">CarMd App</a>
      <a href="/resources">Resources</a>
      <a href="/contactus">Contact Us</a>
    </nav>
    <div class="header__left">
      <img src='./src/images/carmdlogo.png' alt="Logo" class="header__logo">
    </div>
    <div class="header__right">
        <button class="btn btn--primary">Download</button>
    </div>
</header>


<style>

@media (min-width: 1366px) and (max-width: 1920px) {
  /* styles for laptop screens go here */

  /* make the header element take up 80% of the screen width */
  .header {
    width: 40%;
    display: flex;
    position: sticky;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
    padding-inline: 24em;
    /* background-color: #fff; */
  }
}

@media (min-width: 1920px) {
  /* styles for monitor screens go here */

  /* make the header element take up 80% of the screen width */
  .header {
    width: 1920px;
    height: 100px;
    display: absolute;
    position: sticky;
    padding-left: 1em;
    background-color: #fff;
  }
}

  /* .header {
    display: flex;
    position: sticky;
    align-items: center;
    justify-content: center;
    padding-left: 30em;
    flex-wrap: wrap;
  } */

   a {
    margin: 1rem;
   }

  .header__right {
    display: flex;
    align-items: center;
  }

  .header__left{
    display: flex;
    align-items: center;
  }

  .header__logo {
    position: fixed;
    top: 1.5em;
    left: 1em;
  }

  .btn {
    border: none;
    position: fixed;
    top: 2em;
    right: 1em;
  }

  .btn--primary {
    /* background-color: #0074d9; */
    color: #fff;
  }

  .btn--primary:hover {
    background-color: #0088ff;
  }
</style>