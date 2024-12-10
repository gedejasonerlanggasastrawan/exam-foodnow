<template>
    <footer class="footer">
      <div class="container py-5 border-top border-bottom">
        <div class="row">
          <!-- Logo dan Media Sosial -->
          <div class="col-lg-3 mb-5 mb-lg-0">
            <a href="/" class="d-flex mb-4">
              <img
                src="@/assets/img/logo-alt.svg"
                class="img-fluid logo"
                alt="Foodnow Logo"
              />
            </a>
            <h4 class="text-orange">Find Us:</h4>
            <div class="d-flex gap-2">
              <a href="#" class="btn-social">
                <img src="@/assets/img/facebook.svg" alt="Facebook" />
              </a>
              <a href="#" class="btn-social">
                <img src="@/assets/img/instagram.svg" alt="Instagram" />
              </a>
              <a href="#" class="btn-social">
                <img src="@/assets/img/youtube.svg" alt="YouTube" />
              </a>
            </div>
          </div>
  
          <!-- Navigasi -->
          <div class="col-lg-3 mb-5 mb-lg-0">
            <h4 class="text-orange">Navigation</h4>
            <div class="row">
              <div class="col-6">
                <a href="#" class="nav-link">Home</a>
                <a href="#" class="nav-link">Order</a>
                <a href="#" class="nav-link">About</a>
                <a href="#" class="nav-link">Blog</a>
              </div>
              <div class="col-6">
                <a href="#" class="nav-link">Contact</a>
                <a href="#" class="nav-link">Login</a>
                <a href="#" class="nav-link">Register</a>
              </div>
            </div>
          </div>
  
          <!-- Kontak -->
          <div class="col-lg-3 mb-5 mb-lg-0">
            <h4 class="text-orange">Contact</h4>
            <ul>
              <li>
                <img src="@/assets/img/mail.svg" class="contact-icon" alt="Mail" />
                Food.now@mail.com
              </li>
              <li>
                <img src="@/assets/img/phone.svg" class="contact-icon" alt="Phone" />
                +62848477102943
              </li>
              <li>
                <img
                  src="@/assets/img/whatsapp.svg"
                  class="contact-icon"
                  alt="WhatsApp"
                />
                +628184938494
              </li>
            </ul>
          </div>
  
          <!-- Lokasi -->
          <div class="col-lg-3">
            <h4 class="text-orange">Location</h4>
            <ul class="location">
              <li>
                <img
                  src="@/assets/img/location.svg"
                  class="contact-icon"
                  alt="Location"
                />
                <div>
                  <h5>Kerobokan</h5>
                  <p>
                    Jl. Raya Kerobokan Br Taman, Kuta No.98, Kerobokan Kelod, Kec.
                    Kuta Utara, Kabupaten Badung, Bali 80361
                  </p>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
      <div class="container py-3 text-center">
        <p class="copyright">
          Copyright © 2024 Foodnow. All Rights Reserved. Powered by PT. Timedoor
          Indonesia. | Privacy Policy. Protected by Google Privacy Policy and
          Terms of Service.
        </p>
      </div>
    </footer>
  </template>

<style scoped>
.footer {
  font-size: 1.125rem;

  h4 {
    margin-bottom: 1.25rem;
  }

  .nav-link {
    display: block;
    margin-bottom: 0.875rem;
    color: #000;
    text-decoration: none;
    &:hover {
      color: #db8031;
    }
  }

  .btn-social {
    width: 2.5rem;
    height: 2.5rem;
    border-radius: 50%;
    display: inline-flex;
    justify-content: center;
    align-items: center;
    background-color: #f0f0f0;
    transition: background-color 0.3s ease;

    img {
      height: 1.5rem;
      width: 1.5rem;
    }

    &:hover {
      background-color: #db8031;
    }
  }

  .contact-icon {
    height: 1.25rem;
    width: 1.25rem;
    object-fit: contain;
    margin-right: 0.5rem;
  }

  ul {
    list-style: none;
    padding: 0;

    li {
      display: flex;
      align-items: center;
      margin-bottom: 0.875rem;
    }
  }

  .location li {
    align-items: flex-start;

    h5 {
      margin-bottom: 0.5rem;
    }
  }

  .copyright {
    text-align: center;
    max-width: 48.5rem;
    margin: auto;
    font-size: 0.875rem;
    color: #666;
  }

  .text-orange {
    color: #db8031;
  }
}
</style>
