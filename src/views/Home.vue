<template>
<div>
  <header id="header">
    <div class="container">

      <div id="logo" class="pull-left">
        <img src="img/log.png" alt="">
      </div> 

      <nav id="nav-menu-container">
        <ul class="nav-menu">
          <li class="menu-active"><a href="#hero">Home</a></li>
          <li><a href="#about">About Us</a></li>
          <li><a href="#contact">Contact Us</a></li>
          <li><a href="/login">Login</a></li>
        </ul>
      </nav>
    </div>
  </header>

  <section id="hero">
    <div class="hero-container">
      <h1>Welcome to Muncakuy</h1>
      <h2>Bingung cari teman untuk mendaki? Mendaki kok sendirian? Yuk mulai petualanganmu disini!</h2>
      <a href="#about" class="btn-get-started">Get Started</a>
    </div>
  </section>
  <main id="main">
    <section id="about">
      <div class="container">
        <div class="row about-container">
          <div class="col-lg-6 content order-lg-1 order-2">
            <h2 class="title">Yuk ikuti caranya di bawah ini</h2>
            <br>
            <div class="icon-box wow fadeInUp">
              <div class="icon"></div>
              <p class="description">Jika belum memiliki akun, register terlebih dahulu. Jika sudah, anda langsung login saja.</p>
            </div>
            <div class="icon-box wow fadeInUp" data-wow-delay="0.2s">
              <div class="icon"></div>
              <p class="description">Setelah login, kamu bisa mencari teman mendaki yang satu tujuan denganmu</p>
            </div>
            <div class="icon-box wow fadeInUp" data-wow-delay="0.4s">
              <div class="icon"></div>
              <p class="description">Jika sudah menemukan teman, kamu bisa menghubungi nomer handphonenya</p>
            </div>
            <div class="icon-box wow fadeInUp" data-wow-delay="0.6s">
              <div class="icon"></div>
              <p class="description">Jika tidak menemukan teman, maka kamu bisa langsung mengisi form sesuai tujuanmu</p>
            </div>
          </div>
          <div class="col-lg-6 background order-lg-2 order-1 wow fadeInRight"></div>
        </div>
      </div>
    </section>
    <section id="contact">
      <div class="container wow fadeInUp">
        <div class="section-header">
          <h3 class="section-title">Contact</h3>
          <p class="section-description">Ketikkan kritik dan saran anda dengan mengisi form di bawah ini, Terima
            Kasih... </p>
        </div>
      </div>

      <div class="container wow fadeInUp mt-5">
        <div class="row justify-content-center">

          <div class="col-lg-3 col-md-4">

            <div class="info">
              <div>
                <i class="fa fa-map-marker"></i>
                <p>Jln. Danau Ranau, Sawojajar<br>Kota Malang, Jawa Timur, Indonesia</p>
              </div>

              <div>
                <i class="fa fa-envelope"></i>
                <p>munskuy@gmail.com</p>
              </div>

              <div>
                <i class="fa fa-phone"></i>
                <p>+62856-5527-9568</p>
              </div>
            </div>

            <div class="social-links">
              <a href="#" class="twitter"><i class="fa fa-twitter"></i></a>
              <a href="#" class="facebook"><i class="fa fa-facebook"></i></a>
              <a href="#" class="instagram"><i class="fa fa-instagram"></i></a>
              <a href="#" class="google-plus"><i class="fa fa-google-plus"></i></a>
              <a href="#" class="linkedin"><i class="fa fa-linkedin"></i></a>
            </div>

          </div>

          <div class="col-lg-5 col-md-8">
            <div class="form">
              <div id="sendmessage">Your message has been sent. Thank you!</div>
              <div id="errormessage"></div>
              <form action="" method="post" role="form" class="contactForm">
                <div class="form-group">
                  <input type="text" name="name" class="form-control" id="name" placeholder="Your Name"
                    data-rule="minlen:4" data-msg="Please enter at least 4 chars" />
                  <div class="validation"></div>
                </div>
                <div class="form-group">
                  <input type="email" class="form-control" name="email" id="email" placeholder="Your Email"
                    data-rule="email" data-msg="Please enter a valid email" />
                  <div class="validation"></div>
                </div>
                <div class="form-group">
                  <input type="text" class="form-control" name="subject" id="subject" placeholder="Subject"
                    data-rule="minlen:4" data-msg="Please enter at least 8 chars of subject" />
                  <div class="validation"></div>
                </div>
                <div class="form-group">
                  <textarea class="form-control" name="message" rows="5" data-rule="required"
                    data-msg="Please write something for us" placeholder="Message"></textarea>
                  <div class="validation"></div>
                </div>
                <div class="text-center"><button type="submit">Send Message</button></div>
              </form>
            </div>
          </div>

        </div>

      </div>
    </section>
  </main>
  <footer id="footer">
    <div class="container">
      <div class="copyright">
        &copy; Copyright <strong>Muncakuy.com</strong>. All Rights Reserved
      </div>
    </div>
  </footer>
</div>
</template>