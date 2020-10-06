<template>
  <div class="">
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
    <div class="d-flex">
      <div class="sidebar">
        <ul>
          <li>
            <i class="fas fa-envelope-square"></i> Messages
          </li>
          <li>
            <i class="far fa-star"></i> Collections
          </li>
          <li>
            <i class="fas fa-calendar-week"></i> Calender
          </li>
          <span class="side-text">Manage</span>
          <li>
            <i class="fab fa-first-order-alt"></i> Order
          </li>
          <li>
            <i class="fas fa-notes-medical"></i> Giggs
          </li>
          <span class="side-text">Tools</span>
          <li>
            <i class="fas fa-suitcase-rolling"></i> Blog
          </li>
          <li>Blogs</li>
          <li>Add a Blog</li>
          <span class="side-text">Tools</span>
          <li>
            <i class="fas fa-cog"></i> Settings
          </li>
          <li>
            <i class="fas fa-power-off"></i> Logout
          </li>.
        </ul>
      </div>
      <Nuxt />
    </div>
  </div>
</template>
<script>
export default {};
</script>

<style>

.navbar {
  background-color: #fff;
  border-top: 4px solid #000;
  box-shadow: 0px 16px #f2f2f2;
}
.navbar-brand {
  color: #000 !important;
}
.navbar-links li {
  list-style-type: none;
  display: inline-block;
  padding-right: 14px;
}
.side-text {
  color: blue;
}
.sidebar {
  width: 250px;
  background: #fff;
  box-shadow: 0px 16px #f2f2f2;
  height: 80vh;
  position: relative;
}
.sidebar ul {
  padding-top: 1rem;
}
.sidebar ul li {
  list-style: none;
  padding-bottom: 20px;
  font-size: 13px;
}
</style>
