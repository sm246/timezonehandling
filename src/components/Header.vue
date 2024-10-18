<template>
  <header id="header" class="sticky-top">
    <nav class="primary-menu navbar navbar-expand-lg navbar-dropdown-dark">
      <div class="container-fluid">
        <!-- Sidebar Toggler -->
        <button
          id="sidebarCollapse"
          class="navbar-toggler d-block d-md-none"
          type="button"
        >
          <span></span><span class="w-75"></span><span class="w-50"></span>
        </button>

        <!-- Logo -->
        <a class="logo ml-md-3" href="/" title="iDocs Template">
          <img src="./assets/images/logo.png" alt="iDocs Template" />
        </a>
        <span class="text-2 ml-2">v1.0</span>

        <!-- Navbar Toggler -->
        <button
          class="navbar-toggler ml-auto"
          type="button"
          data-toggle="collapse"
          data-target="#header-nav"
        >
          <span></span><span></span><span></span>
        </button>

        <div
          id="header-nav"
          class="collapse navbar-collapse justify-content-end"
        >
          <ul class="navbar-nav">
            <li class="dropdown">
              <a class="dropdown-toggle" href="#">Dropdown</a>
              <ul class="dropdown-menu">
                <li><a class="dropdown-item" href="#">Action</a></li>
                <li class="dropdown">
                  <a class="dropdown-item dropdown-toggle" href="#"
                    >Dropdown Action</a
                  >
                  <ul class="dropdown-menu">
                    <li><a class="dropdown-item" href="#">Action</a></li>
                    <li>
                      <a class="dropdown-item" href="#">Another Action</a>
                    </li>
                  </ul>
                </li>
              </ul>
            </li>
            <li>
              <a href="https://themeforest.net/" target="_blank"
                >Other Template</a
              >
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </header>
</template>

<script>
export default {}
</script>
