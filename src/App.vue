<template>
<header>
<nav class="navbar navbar-expand-lg" style="border-bottom: 1px solid #efefef;">
    <div class="container-fluid">
    <a class="navbar-brand" href="/"><img src="../src/assets/logo.png">YtubeFetch</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <i class="fa fa-ellipsis-h" aria-hidden="true"></i>
    </button>
    <div class="collapse navbar-collapse" role="search" id="navbarSupportedContent">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li class="nav-item">
          <a class="nav-link active" aria-current="page" href="#yt_contents">About</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#FAQ">FAQ</a>
        </li>
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Other Downloaders
          </a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" onclick="showCustomModal()">youtube downloader</a></li>
            <li><a class="dropdown-item" href="facebook.html">Facebook downloader</a></li>
            <li><a class="dropdown-item" onclick="showCustomModal()">instagram downloader</a></li>
            <li><a class="dropdown-item" onclick="showCustomModal()">twitter downloader</a></li>
            <li><a class="dropdown-item" href="pages/downloads.html">My downloads</a></li>
          </ul>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="TOS.html">Terms of service</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
</header>
<router-view/>
</template>

<style>
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50; */
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
