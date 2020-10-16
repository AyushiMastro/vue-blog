<template>
    <b-navbar toggleable="lg" type="dark" variant>
      <b-navbar-brand href="#">Giggs</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="#">Link</b-nav-item>
          <b-button variant="outline-success">Buyer</b-button>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <ul class="navbar-links">
            <li>
              <i class="fas fa-border-all"></i>
            </li>

            <li>
              <i class="fas fa-question-circle"></i>
            </li>
            <li>
              <i class="far fa-bell"></i>
            </li>
            <li>
              <i class="far fa-envelope"></i>
            </li>
          </ul>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>

</template>