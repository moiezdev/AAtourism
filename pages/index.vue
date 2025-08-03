<template>
  <div class="container-fluid">
    <div class="search-form-bg">
      <div class="text">
        <h6>Let's go!</h6>
        <h1>Have a safe journey</h1>
        <h4>Fly to See all destinations</h4>
      </div>
    </div>
<!--    <div class="main-search-form-outer">-->
<!--      <div class="main-search-form">-->
<!--        <div>-->
<!--          <div class="drop-tabs">-->
<!--            <b-tabs>-->
<!--              <b-tab-item label="Flights" icon="airplane-takeoff">-->
<!--                <b-tabs>-->
<!--                  <b-tab active>-->
<!--                    <flightSearchForm />-->
<!--                  </b-tab>-->
<!--                </b-tabs>-->
<!--              </b-tab-item>-->
<!--              <b-tab-item label="Hotel" icon="hotel">-->
<!--                <div class="row search-fileds pt-5">-->
<!--                  <div class="col-lg-9">-->
<!--                    <div class="row">-->
<!--                      <div class="col-lg-12 mt-3">-->
<!--                        <input-->
<!--                          type="text"-->
<!--                          class="form-control index-cntrl"-->
<!--                          placeholder="Destination"-->
<!--                        />-->
<!--                      </div>-->
<!--                      <div class="col-lg-4 col-6 mt-3">-->
<!--                        <div class="date">-->
<!--                          <span class="mdi mdi-calendar"></span>-->
<!--                          <span>Checkin</span>-->
<!--                        </div>-->
<!--                      </div>-->
<!--                      <div class="col-lg-4 col-6 mt-3">-->
<!--                        <div class="date">-->
<!--                          <span class="mdi mdi-calendar"></span>-->
<!--                          <span>Checkout</span>-->
<!--                        </div>-->
<!--                      </div>-->
<!--                      <div class="col-lg-4 mt-3">-->
<!--                        <div class="date">-->
<!--                          <span class="mdi mdi-account-circle"></span>-->
<!--                          <span>2 adult,</span>-->
<!--                          <span class="mdi mdi-bed ml-3"></span>-->
<!--                          <span>Room</span>-->
<!--                        </div>-->
<!--                      </div>-->
<!--                    </div>-->
<!--                  </div>-->
<!--                  <div class="col-lg-3 search-button">-->
<!--                    <router-link-->
<!--                      :to="{ name: 'hotels' }"-->
<!--                      class="search-button-outer"-->
<!--                    >-->
<!--                      <button class="btn btn-light">-->
<!--                        <span>Search for Hotels</span>-->
<!--                        <i class="fa fa-chevron-right"></i>-->
<!--                      </button>-->
<!--                    </router-link>-->
<!--                  </div>-->
<!--                </div>-->
<!--              </b-tab-item>-->
<!--              <b-tab-item label="Car" icon="car">-->
<!--                <div class="row search-fileds pt-5">-->
<!--                  <div class="col-lg-9">-->
<!--                    <div class="row">-->
<!--                      <div class="col-lg-6 mt-3">-->
<!--                        <input-->
<!--                          type="text"-->
<!--                          class="form-control index-cntrl"-->
<!--                          placeholder="Pick Up ?"-->
<!--                        />-->
<!--                      </div>-->

<!--                      <div class="col-lg-6 mt-3">-->
<!--                        <input-->
<!--                          type="text"-->
<!--                          class="form-control index-cntrl"-->
<!--                          placeholder="Drop Off ?"-->
<!--                        />-->
<!--                      </div>-->
<!--                      <div class="col-lg-4 col-6 mt-3">-->
<!--                        <div class="date">-->
<!--                          <span class="mdi mdi-calendar"></span>-->
<!--                          <span>Pick Up</span>-->
<!--                        </div>-->
<!--                      </div>-->
<!--                      <div class="col-lg-4 col-6 mt-3">-->
<!--                        <div class="date">-->
<!--                          <span class="mdi mdi-calendar"></span>-->
<!--                          <span>Drop Off</span>-->
<!--                        </div>-->
<!--                      </div>-->
<!--                      <div class="col-lg-4 mt-3">-->
<!--                        <div class="date">-->
<!--                          <span class="mdi mdi-account-circle"></span>-->
<!--                          <span>1 Pax,</span>-->
<!--                          <span class="mdi mdi-car ml-3"></span>-->
<!--                          <span>Car Type</span>-->
<!--                        </div>-->
<!--                      </div>-->
<!--                    </div>-->
<!--                  </div>-->
<!--                  <div class="col-lg-3 search-button">-->
<!--                    <router-link-->
<!--                      :to="{ name: 'hotels' }"-->
<!--                      class="search-button-outer"-->
<!--                    >-->
<!--                      <button class="btn btn-light">-->
<!--                        <span>Search for Hotels</span>-->
<!--                        <i class="fa fa-chevron-right"></i>-->
<!--                      </button>-->
<!--                    </router-link>-->
<!--                  </div>-->
<!--                </div>-->
<!--              </b-tab-item>-->

<!--              <b-tab-item label="My Booking" icon="ticket-confirmation">-->
<!--                <div class="row search-fileds pt-5">-->
<!--                  <div class="col-lg-9">-->
<!--                    <div class="row">-->
<!--                      <div class="col-lg-6 mt-3">-->
<!--                        <input-->
<!--                          type="text"-->
<!--                          class="form-control index-cntrl"-->
<!--                          placeholder="Ticket number or reservation code (PNR)"-->
<!--                        />-->
<!--                      </div>-->
<!--                      <div class="col-lg-6 mt-3">-->
<!--                        <input-->
<!--                          type="text"-->
<!--                          class="form-control index-cntrl"-->
<!--                          placeholder="Passenger surname"-->
<!--                        />-->
<!--                      </div>-->
<!--                    </div>-->
<!--                  </div>-->
<!--                  <div class="col-lg-3 search-button">-->
<!--                    <router-link-->
<!--                      :to="{ name: 'hotels' }"-->
<!--                      class="search-button-outer"-->
<!--                    >-->
<!--                      <button class="btn btn-light">-->
<!--                        <span>Search for Hotels</span>-->
<!--                        <i class="fa fa-chevron-right"></i>-->
<!--                      </button>-->
<!--                    </router-link>-->
<!--                  </div>-->
<!--                </div>-->
<!--              </b-tab-item>-->
<!--            </b-tabs>-->
<!--          </div>-->
<!--        </div>-->
<!--      </div>-->
<!--    </div>-->
    <div class="content-slogan">
      <h1></h1>
    </div>
    <div class="deals">
      <div class="cheap-deal">
        <h3>International / Domestic Flight Deals</h3>
        <h6>
          “The world is a book, and those who do not travel read only one page”
          Book a lavish flight to your dream destination. Fly with
          <b>AA Travel & Tourism</b> anywhere in the world, at a competitive
          price. We provide you with full service all through your travel trip.
          Get competitive deals on flights, hotel bookings, car rentals and
          anything that make your trip memorable.
        </h6>
        <small>
          <a href="/about">
            Read more
            <span class="mdi mdi-chevron-right"></span>
          </a>
        </small>
      </div>

      <div class="hotel-deals">
        <div class="row">
          <div class="col-lg-12 col-md-12">
            <div class="menulife">
              <a href="/insurance"
                ><img src="../static/manulife.jpg" width="130px" alt
              /></a>
            </div>
          </div>
        </div>
        <div class="row">
          <div class="region">
            <div class="row">
              <div class="col-lg-6 p-0 m-0">
                <div class="row p-2">
                  <div class="col-lg-3 col-sm-3">
                    <div class="region-box asia-bg">
                      <nuxt-link
                    :to="{
                      name: 'packages-id',
                      params: { id: 'asia' },
                    }"
                  >
                      <h2>Asia</h2>
                      </nuxt-link>
                    </div>
                  </div>
                  <div class="col-lg-3 col-sm-3">
                    <div class="region-box midleeast-bg">
                      <nuxt-link
                    :to="{
                      name: 'packages-id',
                      params: { id: 'midle east' },
                    }"
                  >
                      <h2>Middle East</h2>
                      </nuxt-link>
                    </div>
                  </div>
                  <div class="col-lg-3 col-sm-3">
                    <div class="region-box europe-bg">
                      <nuxt-link
                    :to="{
                      name: 'packages-id',
                      params: { id: 'europe' },
                    }"
                  >
                      <h2>Europe</h2>
                      </nuxt-link>
                    </div>
                  </div>
                  <div class="col-lg-3 col-sm-3">
                    <div class="region-box africa-bg">
                       <nuxt-link
                    :to="{
                      name: 'packages-id',
                      params: { id: 'africa' },
                    }"
                  >
                      <h2>Africa</h2>
                       </nuxt-link>
                    </div>
                  </div>
                </div>
              </div>
              <div class="col-lg-6 p-0 m-0">
                <div class="row p-2">
                  <div class="col-lg-3 col-sm-3">
                    <div class="region-box north-america-bg">
                      <nuxt-link
                    :to="{
                      name: 'packages-id',
                      params: { id: 'north america' },
                    }"
                  >
                      <h2>North America</h2>
                      </nuxt-link>
                    </div>
                  </div>
                  <div class="col-lg-3 col-sm-3">
                    <div class="region-box south-america-bg">
                      <nuxt-link
                    :to="{
                      name: 'packages-id',
                      params: { id: 'south america' },
                    }"
                  >
                      <h2>South America</h2>
                      </nuxt-link>
                    </div>
                  </div>
                  <div class="col-lg-3 col-sm-3">
                    <div class="region-box australia-bg">
                       <nuxt-link
                    :to="{
                      name: 'packages-id',
                      params: { id: 'australia' },
                    }"
                  >
                      <h2>Australia</h2>
                       </nuxt-link>
                    </div>
                  </div>
                  <div class="col-lg-3 col-sm-3">
                    <div class="region-box antaractica-bg">
                       <nuxt-link
                    :to="{
                      name: 'packages-id',
                      params: { id: 'antaractica' },
                    }"
                  >
                      <h2>Antarctica</h2>
                       </nuxt-link>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- start of carousel -->
    <div class="ciunteris">
      <h2>SPECIAL OFFERS</h2>
      <h3>Limited-time offers</h3>
      <div class="cont hotel-deals">
        <b-carousel-list :data="allPackages" :items-to-show="slider">
          <template slot="item" slot-scope="list">
            <div class="hotel-deal-box dealbx">
              <div
                v-bind:style="{
                  'background-image':
                    'url(https://fseaatourism.aatourism.ca/assets/' +
                    list.image +
                    ')',
                }"
                class="europe-united"
              ></div>
              <div class="text-area">
                <h2
                  v-html="
                    list.description.length > 150
                      ? list.description.substring(0, 150) + '...'
                      : list.description
                  "
                ></h2>
                <div class="hotel-deal-rate">
                  <div class="left">
                    <h5>
                      {{ list.day != "" ? list.day + " Days" : "" }}
                      {{ list.night != "" ? list.night + " Nights" : "" }}
                      <span class="mdi mdi-chevron-double-right"></span>
                    </h5>
                  </div>
                  <div class="right">
                    <h5>
                      <small>From</small>
                      <span>C$</span> {{ list.price }}
                    </h5>
                  </div>
                </div>
                <div class="hotel-deal-rate">
                  <nuxt-link
                    :to="{
                      name: 'pakagedetails-id',
                      params: { id: list.id },
                    }"
                  >
                    <div class="left">
                      <h5>
                        Package Detail
                        <span class="mdi mdi-chevron-double-right"></span>
                      </h5>
                    </div>
                  </nuxt-link>
                </div>
              </div>
            </div>
          </template>
        </b-carousel-list>
      </div>
    </div>
    <!-- end of carousel -->
    <!-- start of top offer carouse -->
    <!--  <Carousal></Carousal>-->
    <div class="top-baner">
      <div
        class="center-image bottom-slider-box bg-tour-pc"
        alt=""
        :style="{
          backgroundRepeat: 'no-repeat',
          backgroundSize: 'cover',
        }"
      >
        <div class="tp-s">
          <div class="second-title">
            <h2>TOP SERVICES</h2>
          </div>
          <b-carousel-list :data="homeBottomSlides" :items-to-show="1">
            <template slot="item" slot-scope="list">
              <div class="arrow">
                <div class="col-12">
                  <div class="slider-block clearfix slider-tour">
                    <div
                      class="slider-block-left background-block"
                      :style="{
                        backgroundImage:
                          `url(${$config.ASSET_URL}` + list.image + ')',
                      }"
                    ></div>
                    <div class="slider-block-right">
                      <h2 class="sb-title">{{ list.title }}</h2>
                      <div
                        class="sb-price"
                        style="
                          display: -webkit-box;
                          -webkit-line-clamp: 8;
                          -webkit-box-orient: vertical;
                          overflow: hidden;
                        "
                        v-html="list.description"
                      ></div>
                      <div class="sb-text"></div>
                    </div>
                  </div>
                </div>
              </div>
            </template>
          </b-carousel-list>
        </div>
      </div>
    </div>
    <!-- end of top offer carousel -->
    <div class="your-best-deal">
      <div class="heading">
        <div class="container">
          <h4>Your best deal in no time!</h4>
        </div>
      </div>
      <div class="container best-deal-outer">
        <div class="row">
          <div class="col-lg-3 best-deal-box">
            <img src="../static/USP_icon_1.png" width="120px" alt />
            <h6>
              Compare
              <br />800+ Airlines
            </h6>
          </div>
          <div class="col-lg-3 best-deal-box">
            <img src="../static/USP_icon_2.png" width="120px" alt />
            <h6>
              Easy and
              <br />fast booking
            </h6>
          </div>
          <div class="col-lg-3 best-deal-box">
            <img src="../static/USP_icon_3.png" width="120px" alt />
            <h6>
              English speaking
              <br />customer service
            </h6>
          </div>
          <div class="col-lg-3 best-deal-box">
            <img src="../static/USP_icon_4.png" width="120px" alt />
            <h6>
              AA Travel & Tourism is
              <br />a member of IATA
            </h6>
          </div>
        </div>
      </div>
    </div>
    <div class="payment-section">
      <div class="container">
        <div class="row">
          <div class="col-lg-6 mb-4 mt-4">
            <div class="left">
              <h5>AA Travel & Tourism is affiliated with</h5>
              <div class="cards">
                <div>
                  <img src="../static/tico.png" alt="IATA Logo" />
                </div>
                <div>
                  <img src="../static/sabre.png" alt="Sabre Logo" />
                </div>
                <div>
                  <img src="../static/amadeus.png" alt="Amadeus Logo" />
                </div>
                <div>
                  <a
                    href="https://www.igoinsured.com/direct/manulifeglobal.aspx?ag=AATT01"
                    target="_blanck"
                    ><img src="../static/menulife-logo.png" alt="MenuLife Logo"
                  /></a>
                </div>
              </div>
            </div>
          </div>
          <div class="col-lg-6 mb-4 mt-4">
            <div class="right">
              <h5>Secure Payment with</h5>
              <div class="cards">
                <div>
                  <img src="../static/stripe.png" alt="Stripe Logo" />
                </div>
                <div>
                  <img src="../static/paypal.png" alt="PayPal Logo" />
                </div>
                <div>
                  <img src="../static/mastercard.png" alt="Mastercard Logo" />
                </div>
                <div>
                  <img src="../static/visa.png" alt="Visa Card" />
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { mapGetters } from "vuex";
import flightSearchForm from "@/components/flightSearchForm.vue";
import Carousal from "@/components/Carousal.vue";
export default {
  components: {
    flightSearchForm,
    Carousal,
  },

  data() {
    return {
      data:{},
      activeTab: "",
      slider: 3,
      allPackages: [],
      homeBottomSlides: [],
      coverPhoto: "",
      regions: [
        "asia",
        "midle east",
        "europe",
        "africa",
        "north america",
        "south america",
        "australia",
        "antaractica",
      ],
    };
  },
  computed: {
    ...mapGetters({
      pakages: "pakages/getPakages",
      homebottomSlides: "home/getHomeBottomSlides",
      // countriesData: "home/getCountries",
      sliderBottomcoverPhoto: "home/getBottomSliderCoverPhoto",
      // pakageCountry: "pakages/getPakageCountry",
    }),
  },
  created() {
    this.$store.commit("setPnrGenerated",false)
    this.$api.get(`/package`).then(({ data }) => {
      this.$store.commit("pakages/setPakages", data);
      var allPackages = [];
      for (var i = 0; i < 7; i++) {
        allPackages.push(data.data[i]);
      }
      this.allPackages = allPackages;
    });
    if (this.homebottomSlides.length == 0) {
      this.$api.get(`/cmsslider`).then(({ data }) => {
        for (var i = 0; i < data.data.length; i++) {
          if (data.data[i].name == "Home Services Slider") {
            this.sliderTwoId = data.data[i].id;
            this.coverPhoto = data.data[i].cover_photo;
            this.$store.commit("home/setHomeBottomSlider", data.data[i]);
          }
        }
      });
      this.$api.get(`/cmsslide`).then(({ data }) => {
        for (var i = 0; i < data.data.length; i++) {
          if (
            data.data[i].cms_slider_id == this.sliderTwoId &&
            data.data[i].status == "active"
          ) {
            this.homeBottomSlides.push(data.data[i]);
          }
        }
        this.$store.commit("home/setHomeBottomSlides", this.homeBottomSlides);
      });
    } else {
      this.coverPhoto = this.sliderBottomcoverPhoto;
      this.homeBottomSlides = this.homebottomSlides;
    }
     if (this.$auth.loggedIn && this.$auth.strategy.name !== "local") {
      this.checkLogin();
    }
  },
  methods:{
    checkLogin() {
      console.log('this.$auth.user',this.$auth.strategy.name)
      if (this.$auth && this.$auth.strategy &&this.$auth.strategy.name == "google") {
       this.data.first_name = this.$auth.user.given_name;
        this.data.last_name = this.$auth.user.family_name;
        this.data.email = this.$auth.user.email;
        this.data.provider_id = this.$auth.user.sub;
        this.data.provider = this.$auth.strategy.name;
        this.$api({
          method: "post",
          url: "/user/social",
          data: this.data,
        })
        .then(({ data }) => {
          this.$auth.$storage.setLocalStorage("strategy", "local");
          this.$auth.$storage.setLocalStorage("_token.google", false);
          this.$auth.$storage.setLocalStorage(
            "_token.local",
            "Bearer " + data.data.token
          );
          this.$auth.$storage.setCookie("strategy", "local");
          this.$auth.$storage.setCookie("_token.google", false);
          this.$auth.$storage.setCookie(
            "_token.local",
            "Bearer " + data.data.token
          );
          // return (window.location.href = this.DashboardUrl);
          // this.$router.push("/profile");
          window.location.reload();
        });
      }
      if (this.$auth.strategy.name == "facebook") {
        if (!this.$auth.user.email) {
          alert("Please add email address to continue!");
          this.$router.push("/login");
          this.$auth.$storage.removeLocalStorage("strategy");
          this.$auth.$storage.removeLocalStorage("_token.local");
          this.$auth.$storage.removeCookie("strategy");
          this.$auth.$storage.removeCookie("_token.local");
        } else {
          this.data.first_name = this.$auth.user.name;
          this.data.last_name = this.$auth.user.name;
          this.data.email = this.$auth.user.email;
          this.data.provider_id = this.$auth.user.id;
          this.data.provider = this.$auth.strategy.name;
          this.$api.post(`/user/social`, this.data).then(({ data }) => {
            this.$auth.$storage.setLocalStorage("strategy", "local");
            this.$auth.$storage.setLocalStorage("_token.facebook", false);
            this.$auth.$storage.setLocalStorage(
              "_token.local",
              "Bearer " + data.data.token
            );
            this.$auth.$storage.setCookie("strategy", "local");
            this.$auth.$storage.setCookie("_token.facebook", false);
            this.$auth.$storage.setCookie(
              "_token.local",
              "Bearer " + data.data.token
            );
            // this.$router.push("/profile");
            window.location.reload();
          });
        }
      }
    },
  convertToCapital(string){
    console.log('string',string.cap)
  }
  }
};
</script>

