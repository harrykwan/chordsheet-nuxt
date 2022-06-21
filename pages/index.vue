<template>
  <div>
    <FooterNav />
    <div class="header header-fixed header-logo-center header-auto-show">
      <a href="index.html" class="header-title">
        <img class="toplogo" src="images/buskking-yellow.png" />
        <span>BUSKKING</span></a
      >

      <!-- <a href="#" data-back-button class="header-icon header-icon-1"
        ><i class="fas fa-arrow-left"></i
      ></a>
      <a href="#" data-toggle-theme class="header-icon header-icon-4"
        ><i class="fas fa-lightbulb"></i
      ></a> -->
    </div>

    <div class="page-content header-clear pb-3">
      <div
        class="card position-fixed w-100"
        data-card-height="400"
        style="
          background: none;
          background-image: url('images/guitar.jpg');
          margin-top: -50px;
        "
      >
        <div
          style="
            width: 100%;
            height: 100%;
            position: inherit;
            background: rgba(0, 0, 0, 0.7);
          "
        >
          <img class="biglogo" src="images/buskking-yellow.png" />
        </div>

        <div class="card-bottom disabled mb-5 pb-3 mt-2 text-center">
          <a
            href="#"
            data-menu="menu-share"
            class="mx-2 icon icon-xs rounded-s bg-blue2-dark"
            ><i class="fa fa-share-alt"></i
          ></a>
          <a
            href="#"
            data-menu="menu-share"
            class="mx-2 icon icon-xs rounded-s bg-red2-dark"
            ><i class="fa fa-bookmark"></i
          ></a>
        </div>
        <div class="card-top mb-5 pb-3 mt-2 text-center"></div>
        <div class="card-overlay bg-gradient opacity-10"></div>
      </div>
      <div
        class="card border-0 shadow-0 bg-transparent no-click"
        data-card-height="320"
      ></div>

      <div class="card card-style mx-0 mb-0 pb-5">
        <div
          class="divider mx-auto mt-3 bg-gray-dark opacity-30 rounded-s mb-n1"
          style="height: 5px; width: 50px"
        ></div>
        <div class="content">
          <div class="card card-style" data-card-height="170">
            <div class="card-top p-2">
              <!-- <a
            href="#"
            class="btn btn-xs bg-white color-black font-700 text-uppercase rounded-s"
            >Start</a
          > -->
            </div>

            <div class="card-bottom p-3">
              <h1 class="color-white mb-n1">男歌手</h1>
              <p class="color-white mb-0 opacity-60">Click Me</p>
            </div>
            <div class="card-overlay bg-gradient"></div>
          </div>

          <div class="d-flex">
            <div class="me-auto">
              <span
                class="badge no-click bg-green-dark p-2 text-uppercase rounded-s mb-3"
                >VACATION</span
              >
            </div>
            <div class="mx-auto">
              <span class="opacity-50 font-12"
                ><i class="far fa-calendar-alt pe-2"></i>21st Aug - 28 Aug</span
              >
            </div>
            <div class="mx-auto">
              <span class="opacity-50 font-12"
                ><i class="far fa-heart pe-2"></i>25k</span
              >
            </div>
          </div>
          <h1 class="font-24 line-height-m pb-1">Maldives Summer Holliday</h1>
          <p class="pt-1">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Curabitur
            aliquam non nunc quis maximus. Fusce volutpat arcu id ante maximus
            vestibulum. Curabitur non nisi venenatis, pharetra nisl et,
            ullamcorper diam. Morbi interdum varius molestie. Quisque feugiat
            augue id diam ornare auctor.
          </p>
          <div class="d-flex pb-2">
            <a
              href="#"
              class="mx-auto shareToFacebook icon icon-xs rounded-sm bg-facebook"
              ><i class="fab fa-facebook-f"></i
            ></a>
            <a
              href="#"
              class="mx-auto shareToTwitter icon icon-xs rounded-sm bg-twitter"
              ><i class="fab fa-twitter"></i
            ></a>
            <a
              href="#"
              class="mx-auto shareToWhatsApp icon icon-xs rounded-sm bg-whatsapp"
              ><i class="fab fa-whatsapp"></i
            ></a>
            <a
              href="#"
              class="mx-auto shareToLinkedIn icon icon-xs rounded-sm bg-linkedin"
              ><i class="fab fa-linkedin-in"></i
            ></a>
            <a
              href="#"
              class="mx-auto shareToMail icon icon-xs rounded-sm bg-mail"
              ><i class="fa fa-envelope"></i
            ></a>
          </div>
        </div>

        <div class="divider divider-margins"></div>

        <div
          class="card card-style bg-17"
          data-card-height="400"
          style="background-image: url('images/travel/4m.jpg')"
        >
          <div class="card-center text-center">
            <h2 class="color-white pt-2">"Something I'll never forget"</h2>
            <a href="#" class="color-white">Jack Son - Tourist</a>
          </div>
          <div class="card-overlay bg-black opacity-60"></div>
        </div>

        <div class="divider divider-margins"></div>

        <div class="content mt-0">
          <h4>This is an Image Gallery</h4>
          <p>
            This page is not WordPress, it's an HTML website. Yes, that's right.
            but you can convert it to WordPress yourself or hire an expert from
            Envato Studio.
          </p>
          <div class="row mb-0">
            <div class="col-4">
              <a
                href="images/travel/1m.jpg"
                class="default-link"
                data-gallery="gallery-1"
                title="Image Title or Caption"
              >
                <img
                  src="images/empty.png"
                  data-src="images/travel/1s.jpg"
                  class="preload-img shadow-s img-fluid rounded-s"
                  alt="img"
                />
              </a>
            </div>
            <div class="col-4">
              <a
                href="images/travel/4m.jpg"
                class="default-link"
                data-gallery="gallery-1"
                title="Image Title or Caption"
              >
                <img
                  src="images/empty.png"
                  data-src="images/travel/4s.jpg"
                  class="preload-img shadow-s img-fluid rounded-s"
                  alt="img"
                />
              </a>
            </div>
            <div class="col-4">
              <a
                href="images/travel/8m.jpg"
                class="default-link"
                data-gallery="gallery-1"
                title="Image Title or Caption"
              >
                <img
                  src="images/empty.png"
                  data-src="images/travel/8s.jpg"
                  class="preload-img shadow-s img-fluid rounded-s"
                  alt="img"
                />
              </a>
            </div>
          </div>
        </div>

        <div class="divider divider-margins"></div>

        <div
          class="card card-style bg-28"
          style="background-image: url('images/travel/6m.jpg')"
        >
          <div class="card-body my-3">
            <h1 class="color-white">
              Location Live
              <br />Walkthrough
            </h1>
            <p class="color-white opacity-60 mb-0">
              We are here to show off the brand new Apple Watch Release. Join us
              and watch it live!
            </p>
            <a
              href="#"
              class="btn btn-s rounded-sm bg-highlight color-white mt-3 text-uppercase font-800"
              ><i class="fa fa-play-circle pe-2"></i> WATCH LIVE</a
            >
          </div>
          <div class="card-overlay bg-black opacity-70"></div>
        </div>

        <div class="divider divider-margins"></div>

        <div class="footer">
          <a href="#" class="footer-title"
            ><span class="color-highlight">StickyMobile</span></a
          >
          <p class="footer-text">
            <span
              >Made with
              <i class="fa fa-heart color-highlight font-16 ps-2 pe-2"></i> by
              Enabled</span
            ><br /><br />Powered by the best Mobile Website Developer on Envato
            Market. Elite Quality. Elite Products.
          </p>
          <div class="text-center mb-3">
            <a
              href="#"
              class="icon icon-xs rounded-sm shadow-l me-1 bg-facebook"
              ><i class="fab fa-facebook-f"></i
            ></a>
            <a href="#" class="icon icon-xs rounded-sm shadow-l me-1 bg-twitter"
              ><i class="fab fa-twitter"></i
            ></a>
            <a href="#" class="icon icon-xs rounded-sm shadow-l me-1 bg-phone"
              ><i class="fa fa-phone"></i
            ></a>
            <a
              href="#"
              data-menu="menu-share"
              class="icon icon-xs rounded-sm me-1 shadow-l bg-red-dark"
              ><i class="fa fa-share-alt"></i
            ></a>
            <a
              href="#"
              class="back-to-top icon icon-xs rounded-sm shadow-l bg-dark-light"
              ><i class="fa fa-angle-up"></i
            ></a>
          </div>
          <p class="footer-copyright">
            Copyright &copy; Enabled <span id="copyright-year">2017</span>. All
            Rights Reserved.
          </p>
          <p class="footer-links">
            <a href="#" class="color-highlight">Privacy Policy</a> |
            <a href="#" class="color-highlight">Terms and Conditions</a> |
            <a href="#" class="back-to-top color-highlight"> Back to Top</a>
          </p>
          <div class="clear"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const loading = useLoadingScreen();
loading.value = true;
onMounted(() => {
  if (process.client) {
    setTimeout(() => {
      try {
        init_template();
        loading.value = false;
      } catch (e) {
        console.log(e);
        loading.value = false;
      }
    }, 100);
  }
});
</script>

<style scoped>
.toplogo {
  width: 80px;
  margin-top: -18px;
  height: 54px;
  object-fit: cover;
  object-position: top;
  padding-top: 10px;
  margin-right: -15px;
}

.header-title {
  margin-left: -85px;
}

.biglogo {
  position: inherit;
  width: 300px;
  /* height: 300px;
  object-fit: cover; */
  /* backdrop-filter: blur(10px); */
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
  border: 0px solid black;
  border-radius: 50%;
  /* background: black; */
}
</style>
