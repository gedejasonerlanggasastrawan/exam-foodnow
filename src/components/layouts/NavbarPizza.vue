<template>
  <div>
    <!-- Navbar -->
    <nav class="navbar fixed-top navbar-dark navbar-expand-lg custom-navbar" :class="{ 'navbar-scrolled': isScrolled }">
      <div class="container d-flex align-items-center">
        <!-- Logo -->
        <a href="/" class="logo d-flex align-items-center me-5">
          <img src="@/assets/img/logo.svg" alt="Logo" class="logo" />
        </a>

        <!-- Toggler -->
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#collapsingNavbar3"
        >
          <span class="navbar-toggler-icon"></span>
        </button>

        <!-- Navbar Menu -->
        <div class="navbar-collapse collapse w-100" id="collapsingNavbar3">
          <ul class="navbar-nav mx-auto">
            <li class="nav-item">
              <a class="nav-link" href="#">Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Order</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">About</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Blog</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Contact us</a>
            </li>
          </ul>

          <!-- Right Aligned Buttons -->
          <ul class="nav navbar-nav ms-auto d-flex align-items-center">
            <li class="nav-item me-3">
              <a class="nav-link text-white" href="#">Login</a>
            </li>
            <li class="nav-item">
              <button class="btn custom-register-btn">Register</button>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <div class="hero">
      <h1 class="hero-title">Pizza order</h1>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isScrolled: false, // Untuk mendeteksi apakah halaman di-scroll
    };
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
  },
  beforeUnmount() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    handleScroll() {
      this.isScrolled = window.scrollY > 50; // Navbar berubah setelah scroll lebih dari 50px
    },
  },
};
</script>

<style scoped>
/* Navbar Styling */
.navbar {
  transition: background-color 0.3s ease;
}

.custom-navbar {
  background: rgba(0, 0, 0, 0.5); /* Default transparan */
}

.navbar-scrolled {
  background: black; /* Background solid saat scroll */
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
}

.navbar-nav .nav-item .nav-link {
  padding: 0.5rem 1rem;
  font-size: 16px;
  font-weight: 500;
  color: white;
  transition: color 0.3s ease;
}

.navbar-nav .nav-item .nav-link:hover {
  color: #db8031;
}

.logo {
  height: 50px;
  width: 200px;
}

/* Register Button */
.custom-register-btn {
  background-color: #db8031;
  color: white;
  border-radius: 20px;
  transition: background-color 0.3s ease;
}

.custom-register-btn:hover {
  background-color: #db8031;
}

/* Mobile Dropdown Styling */
.navbar-collapse .nav-item {
  text-align: center; /* Rapi untuk tampilan mobile */
  margin-bottom: 10px;
}

.navbar-collapse .nav-link {
  padding: 10px;
}

/* Hero Section Styling */
.hero {
  background: url("@/assets/img/hero.png") no-repeat center center;
  background-size: cover;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

.hero::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  z-index: -1;
}

.hero-title {
  font-size: 60px;
  font-weight: bold;
  text-shadow: 2px 2px 4px #000000;
  color: #db8031;
  text-align: center;
}
</style>
