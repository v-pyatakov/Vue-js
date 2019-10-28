<template>
  <div id="app" class="wrap">
    <header class="header flex">
      <ul class="nav flex">
        <router-link tag="li" to="/" ><a>Home</a></router-link>
        <router-link tag="li" to="/about" ><a>About</a></router-link>
        <router-link tag="li" to="/todo" ><a>Todo</a></router-link>
      </ul>
    </header>
    <router-view/>
  </div>
</template>

<style>
  #app {
    font-family: 'Consolas', Arial;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }
  .flex{
    display:flex;
    flex-wrap:wrap;
    flex-direction:row;
  }
  .header {
    justify-content:center;
    align-items:center;
    width: 100%;
    height: 50px;
    background-color: #000000;
  }
  .nav>li {
    margin:0  30px;
    padding:5px 0;
  }
  .nav>li:hover {
    border-bottom: 1px solid #ffffff;
  }
  .nav>li>a {
    color: #ffffff;
    text-transform: capitalize;
  }
  .router-link-exact-active{
    border-bottom: 1px solid #ffffff;
  }
</style>
