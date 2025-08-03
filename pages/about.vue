<template>
  <div class="container-fluid flight-list-body">
    <div class="flights-page">
      <div class="page-heading">
        <div class="container">
          <div class="flights-modify-section">
            <div class="left">
              <div
                class="flight-top-section"
                style="width: 100%; justify-content: center"
              >
                <h1>About Us</h1>
                <!-- <span class="mdi mdi-airplane mdi-rotate-90"></span> -->
              </div>
              <h5>Home/About Us</h5>
            </div>
            <!-- <div>
              <div class="right">
                <button class="btn btn-primary">Change your flight</button>
              </div>
            </div> -->
          </div>
        </div>
      </div>

      <!-- <div class="content-slogan">
        <h1>Cheap Flights</h1>
        <h6>
          Home
          <span class="mdi mdi-chevron-double-right"></span>
          <a href>Flights</a>
        </h6>
      </div> -->
      <div class="contact-content pt-2">
        <!-- <div class="cheap-deal">
        <h3>International / Domestic Flight Deals</h3>
        <h6>Fancy flights to Venice for a romantic weekend away or how about flights to Oslo in Norway to see how a nation deals with a real winter? Wherever you want to fly in the world, AA Tourism Canada offers you the lowest prices on the web, and all it takes is just a few clicks.</h6>
        <small>
          Read more
          <span class="mdi mdi-chevron-down"></span>
        </small>
      </div> -->
        <div class="contact-main">
            <div class="row">
                <div class="col-lg-6">
                    <div class="simple-text" style="text-align: left">
                        <h1 class="underline2" style="text-align: left;">
                            {{aboutUs.value}}
                        </h1>
                        <h4 class="color-grey">
                        </h4>
                        <br />
                        <span v-html="aboutUs.description" class="color-grey" >
                        </span>
                    </div>
                </div>
                <div class="col-lg-6">
                    <div class="about-detail-box">
                        <img
                        :src="
                          aboutUs.image ? `${$config.ASSET_URL}${aboutUs.image}` : ''"
                        alt=""
                        />
                    </div>
                </div>


                
            </div>
        </div>
        
      </div>
      <div class="contact-form">
        <div class="contact-main">
            <div class="row">
                <div class="col-lg-12">
                    <div class="second-title">
                        <h2 class="subtitle">{{whyUs.name}}</h2>
                        <p class="color-grey" v-html="whyUs.description"></p>
                        
                    </div>
                </div>
                <div v-if="why_us_bwu_1.image" class="col-lg-3">
                    <div class="icon-block style-5">
                        <div  class="icon-img">
                          <img :src="why_us_bwu_1.image ? `${$config.ASSET_URL}${why_us_bwu_1.image}` : ''" alt="">
                        </div>
                        <div class="icon-text color-dark-2-light" v-html="why_us_bwu_1.description.length > limit ? why_us_bwu_1.description.substring(0,limit)+'...' : why_us_bwu_1.description">
                        </div>
                    </div>
                </div>
                <div v-if="why_us_bwu_2.image" class="col-lg-3">
                    <div class="icon-block style-5">
                        <img :src="why_us_bwu_2.image ? `${$config.ASSET_URL}${why_us_bwu_2.image}` : ''" alt="" class="icon-img">
                        <div class="icon-text color-dark-2-light" v-html="why_us_bwu_2.description.length > limit ? why_us_bwu_2.description.substring(0,limit)+'...' : why_us_bwu_2.description">
                        </div>
                    </div>
                </div>
                <div v-if="why_us_bwu_3.image" class="col-lg-3">
                    <div class="icon-block style-5">
                        <img :src="why_us_bwu_3.image ? `${$config.ASSET_URL}${why_us_bwu_3.image}` : ''" alt="" class="icon-img">
                        <div class="icon-text color-dark-2-light" v-html="why_us_bwu_3.description.length > limit ? why_us_bwu_3.description.substring(0,limit)+'...' : why_us_bwu_3.description">
                        </div>
                    </div>
                </div>
                <div v-if="why_us_bwu_4.image" class="col-lg-3">
                    <div class="icon-block style-5">
                        <img :src="why_us_bwu_4.image ? `${$config.ASSET_URL}${why_us_bwu_4.image}` : ''" alt="" class="icon-img">
                        <div class="icon-text color-dark-2-light" v-html="why_us_bwu_4.description.length > limit ? why_us_bwu_4.description.substring(0,limit)+'...' : why_us_bwu_4.description">
                        </div>
                    </div>
                </div>
                <div v-if="why_us_bwu_5.image" class="col-lg-3">
                    <div class="icon-block style-5">
                        <img :src="why_us_bwu_5.image ? `${$config.ASSET_URL}${why_us_bwu_5.image}` : ''" alt="" class="icon-img">
                        <div class="icon-text color-dark-2-light" v-html="why_us_bwu_5.description.length > limit ? why_us_bwu_5.description.substring(0,limit)+'...' : why_us_bwu_5.description">
                        </div>
                    </div>
                </div>
                <div v-if="why_us_bwu_6.image" class="col-lg-3">
                    <div class="icon-block style-5">
                        <img :src="why_us_bwu_6.image ? `${$config.ASSET_URL}${why_us_bwu_6.image}` : ''" alt="" class="icon-img">
                        <div class="icon-text color-dark-2-light" v-html="why_us_bwu_6.description.length > limit ? why_us_bwu_6.description.substring(0,limit)+'...' : why_us_bwu_6.description">
                        </div>
                    </div>
                </div>
                <div v-if="why_us_bwu_7.image" class="col-lg-3">
                    <div class="icon-block style-5">
                        <img :src="why_us_bwu_7.image ? `${$config.ASSET_URL}${why_us_bwu_7.image}` : ''" alt="" class="icon-img">
                        <div class="icon-text color-dark-2-light" v-html="why_us_bwu_7.description.length > limit ? why_us_bwu_7.description.substring(0,limit)+'...' : why_us_bwu_7.description">
                        </div>
                    </div>
                </div>
                <div v-if="why_us_bwu_8.image" class="col-lg-3">
                    <div class="icon-block style-5">
                        <img :src="why_us_bwu_8.image ? `${$config.ASSET_URL}${why_us_bwu_8.image}` : ''" alt="" class="icon-img">
                        <div class="icon-text color-dark-2-light" v-html="why_us_bwu_8.description.length > limit ? why_us_bwu_8.description.substring(0,limit)+'...' : why_us_bwu_8.description">
                        </div>
                    </div>
                </div>
                <div v-if="why_us_bwu_9.image" class="col-lg-3">
                    <div class="icon-block style-5">
                        <img :src="why_us_bwu_9.image ? `${$config.ASSET_URL}${why_us_bwu_9.image}` : ''" alt="" class="icon-img">
                        <div class="icon-text color-dark-2-light" v-html="why_us_bwu_9.description.length > limit ? why_us_bwu_9.description.substring(0,limit)+'...' : why_us_bwu_9.description">
                        </div>
                    </div>
                </div>
            </div>
        </div>
      </div>
      <div class="testimonials-heading">
        <div class="heading">
          <h3>WHAT OUR CUSTOMER SAY?</h3>
        </div>
        <div class="container best-deal-outer">
          <div class="row">
            <div :key="index" v-for="(user_feedback, index) in feedBacks" class="col-lg-4 testimonials">
                <figure class="snip1192">
                    <blockquote>
                        <p>{{user_feedback.message}}</p>
                    </blockquote>
                    <div class="author">
                        <img :src="user_feedback.image ? `${$config.ASSET_URL}${user_feedback.image}` : ''">
                        <h5>{{user_feedback.name}}
                            <span>
                                <div class="testimonial-stars">
                                    <span :key="index" v-for="(number, index) in parseInt(user_feedback.rating)" class="mdi mdi-star star"></span>
                                </div>
                            </span>
                        </h5>
                    </div>
                </figure>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- flight-detail-section -->
    <b-sidebar
      id="sidebar-backdrop"
      class="flight-detail-bar"
      :backdrop-variant="variant"
      backdrop
      right
      shadow
      title="Flight Detail"
    >
      <div class="flight-detail-fare-section">
        <div class="button-box">
          <div class="price">
            <small>C$</small>
            <span>2,496</span>
            <sup>.75</sup>
            <h6>Per Person</h6>
            <div class="book-btn">
              <router-link
                :to="{ name: 'passengerdetail' }"
                class="search-button-outer"
              >
                <button class="btn btn-dark">
                  Book this Flight
                  <i class="fa fa-arrow-right"></i>
                </button>
              </router-link>
            </div>
          </div>
        </div>
        <div class="luggage-detail">
          <div>
            <span class="mdi mdi-briefcase-check"></span>
          </div>
          <div>
            <span> 30kg Luggage </span>
          </div>
          <div>
            <span class="mdi mdi-ticket-confirmation"></span>
          </div>
          <div>
            <span>Economy</span>
          </div>
        </div>
        <div class="outbound">
          <div class="icon">
            <span class="mdi mdi-airplane mdi-rotate-90"></span>
          </div>
          <div class="text">
            <h5>Outbound, We 05 Aug</h5>
            <span>Duration: 13h15m</span>
          </div>
        </div>
        <div class="flight-full-summary">
          <div class="time">
            <div>
              <strong>03:10</strong>
              <h6>05 Aug</h6>
            </div>
            <div>
              <strong>03:10</strong>
              <h6>05 Aug</h6>
            </div>
          </div>
          <div class="center-line">
            <div class="x-line-dot"></div>
            <div class="x-line"></div>
            <div class="x-line-dot"></div>
          </div>
          <div class="your-flight">
            <strong>Lahore</strong>
            <h6>(LHE), Pakistan</h6>
            <div class="facilities">
              <h6>Emirates EK623</h6>
              <div class="facilitie-box">
                <div>
                  <span class="mdi mdi-seat-recline-normal"></span>
                </div>
                <div>
                  <small>32" seat pitch</small>
                </div>
              </div>
              <div class="facilitie-box">
                <div>
                  <span class="mdi mdi-video"></span>
                </div>
                <div>
                  <small>Seatback on-demand video</small>
                </div>
              </div>
              <div class="facilitie-box">
                <div>
                  <span class="mdi mdi-wifi"></span>
                </div>
                <div>
                  <small>Basic web browsing (fee)</small>
                </div>
              </div>
              <div class="facilitie-box">
                <div>
                  <span class="mdi mdi-power-plug mdi-rotate-90"></span>
                </div>
                <div>
                  <small>Power & USB outlets</small>
                </div>
              </div>
              <div class="facilitie-box">
                <div>
                  <span class="mdi mdi-food-fork-drink"></span>
                </div>
                <div>
                  <small>Meal provided</small>
                </div>
              </div>
              <div class="flight-class">
                <div class="flight-class-box">
                  <div>
                    <label for>Class:</label>
                  </div>
                  <div>
                    <span>Economy</span>
                  </div>
                </div>
                <div class="flight-class-box">
                  <div>
                    <label for>Aircraft:</label>
                  </div>
                  <div>
                    <span>Boeing 777-300ER</span>
                  </div>
                </div>
                <div class="flight-class-box">
                  <div>
                    <label for>Distance</label>
                  </div>
                  <div>
                    <span>1988 Kms</span>
                  </div>
                </div>
              </div>
            </div>
            <strong>Lahore</strong>
            <h6>(LHE), Pakistan</h6>
          </div>
        </div>
        <div class="outbound">
          <div class="icon">
            <span class="mdi mdi-airplane mdi-rotate-90"></span>
          </div>
          <div class="text">
            <h5>Inbound, We 05 Aug</h5>
            <span>Duration: 13h15m</span>
          </div>
        </div>
        <div class="flight-full-summary">
          <div class="time">
            <div>
              <strong>03:10</strong>
              <h6>05 Aug</h6>
            </div>
            <div>
              <strong>03:10</strong>
              <h6>05 Aug</h6>
            </div>
          </div>
          <div class="center-line">
            <div class="x-line-dot"></div>
            <div class="x-line"></div>
            <div class="x-line-dot"></div>
          </div>
          <div class="your-flight">
            <strong>Lahore</strong>
            <h6>(LHE), Pakistan</h6>
            <div class="facilities">
              <h6>Emirates EK623</h6>
              <div class="facilitie-box">
                <div>
                  <span class="mdi mdi-seat-recline-normal"></span>
                </div>
                <div>
                  <small>32" seat pitch</small>
                </div>
              </div>
              <div class="facilitie-box">
                <div>
                  <span class="mdi mdi-video"></span>
                </div>
                <div>
                  <small>Seatback on-demand video</small>
                </div>
              </div>
              <div class="facilitie-box">
                <div>
                  <span class="mdi mdi-wifi"></span>
                </div>
                <div>
                  <small>Basic web browsing (fee)</small>
                </div>
              </div>
              <div class="facilitie-box">
                <div>
                  <span class="mdi mdi-power-plug mdi-rotate-90"></span>
                </div>
                <div>
                  <small>Power & USB outlets</small>
                </div>
              </div>
              <div class="facilitie-box">
                <div>
                  <span class="mdi mdi-food-fork-drink"></span>
                </div>
                <div>
                  <small>Meal provided</small>
                </div>
              </div>
              <div class="flight-class">
                <div class="flight-class-box">
                  <div>
                    <label for>Class:</label>
                  </div>
                  <div>
                    <span>Economy</span>
                  </div>
                </div>
                <div class="flight-class-box">
                  <div>
                    <label for>Aircraft:</label>
                  </div>
                  <div>
                    <span>Boeing 777-300ER</span>
                  </div>
                </div>
                <div class="flight-class-box">
                  <div>
                    <label for>Distance</label>
                  </div>
                  <div>
                    <span>1988 Kms</span>
                  </div>
                </div>
              </div>
            </div>
            <strong>Lahore</strong>
            <h6>(LHE), Pakistan</h6>
          </div>
        </div>
      </div>
    </b-sidebar>
    <!-- flight-detail-section -->
  </div>
</template>
<script>
import { mapGetters } from "vuex";

export default {
  auth: false,
  
  data() {
    return {
      value: "250",
      limit: 50,
      aboutUs: {},
      whyUs: {},
      feedBacks: [],
      our_story_bb_1: {},
      our_story_bb_2: {},
      our_story_bb_3: {},
      why_us_bwu_1: {'description': ''},
      why_us_bwu_2: {'description': ''},
      why_us_bwu_3: {'description': ''},
      why_us_bwu_4: {'description': ''},
      why_us_bwu_5: {'description': ''},
      why_us_bwu_6: {'description': ''},
      why_us_bwu_7: {'description': ''},
      why_us_bwu_8: {'description': ''},
      why_us_bwu_9: {'description': ''},
    };
  },

  computed: {
    ...mapGetters({
      siteSetting: "siteSetting/getSetting",
      Feedback: "siteSetting/getFeedback",
    }),
  },

  created() {
    if (this.Feedback == undefined) {
      this.$api.get(`/userfeedback`).then(({ data }) => {
        this.feedBacks = data.data;
        this.$store.commit("siteSetting/setFeedback", data.data);
      });
    } else {
      this.feedBacks = this.Feedback;
    }

    if (this.siteSetting == undefined) {
      this.loading = true;
      this.$api.get(`/setting`).then(({ data }) => {
        for (var i = 0; i < data.data.length; i++) {
          if (data.data[i].key == "about-us") {
            this.aboutUs = data.data[i];
          }
        }
        this.loading = false;
      });
    } else {
      for (var i = 0; i < this.siteSetting.length; i++) {
        if (this.siteSetting[i].key == "about-us") {
          this.aboutUs = this.siteSetting[i];
        }
      }
    }
    if (this.siteSetting == undefined) {
      this.$api.get(`/setting`).then(({ data }) => {
        for (var i = 0; i < data.data.length; i++) {
          if (data.data[i].key == "why_us") {
            this.whyUs = data.data[i];
          } else if (data.data[i].key == "our_story_bottom_box_1") {
            this.our_story_bb_1 = data.data[i];
          } else if (data.data[i].key == "our_story_bottom_box_2") {
            this.our_story_bb_2 = data.data[i];
          } else if (data.data[i].key == "our_story_bottom_box_3") {
            this.our_story_bb_3 = data.data[i];
          } else if (data.data[i].key == "why_book_with_us_box_1") {
            this.why_us_bwu_1 = data.data[i];
          } else if (data.data[i].key == "why_book_with_us_box_2") {
            this.why_us_bwu_2 = data.data[i];
          } else if (data.data[i].key == "why_book_with_us_box_3") {
            this.why_us_bwu_3 = data.data[i];
          } else if (data.data[i].key == "why_book_with_us_box_4") {
            this.why_us_bwu_4 = data.data[i];
          } else if (data.data[i].key == "why_book_with_us_box_5") {
            this.why_us_bwu_5 = data.data[i];
          } else if (data.data[i].key == "why_book_with_us_box_6") {
            this.why_us_bwu_6 = data.data[i];
          } else if (data.data[i].key == "why_book_with_us_box_7") {
            this.why_us_bwu_7 = data.data[i];
          } else if (data.data[i].key == "why_book_with_us_box_8") {
            this.why_us_bwu_8 = data.data[i];
          } else if (data.data[i].key == "why_book_with_us_box_9") {
            this.why_us_bwu_9 = data.data[i];
          }
        }
      });
    } else {
      for (var i = 0; i < this.siteSetting.length; i++) {
        if (this.siteSetting[i].key == "why_us") {
          this.whyUs = this.siteSetting[i];
        } else if (this.siteSetting[i].key == "our_story_bottom_box_1") {
          this.our_story_bb_1 = this.siteSetting[i];
        } else if (this.siteSetting[i].key == "our_story_bottom_box_2") {
          this.our_story_bb_2 = this.siteSetting[i];
        } else if (this.siteSetting[i].key == "our_story_bottom_box_3") {
          this.our_story_bb_3 = this.siteSetting[i];
        } else if (this.siteSetting[i].key == "why_book_with_us_box_1") {
          this.why_us_bwu_1 = this.siteSetting[i];
        } else if (this.siteSetting[i].key == "why_book_with_us_box_2") {
          this.why_us_bwu_2 = this.siteSetting[i];
        } else if (this.siteSetting[i].key == "why_book_with_us_box_3") {
          this.why_us_bwu_3 = this.siteSetting[i];
        } else if (this.siteSetting[i].key == "why_book_with_us_box_4") {
          this.why_us_bwu_4 = this.siteSetting[i];
        } else if (this.siteSetting[i].key == "why_book_with_us_box_5") {
          this.why_us_bwu_5 = this.siteSetting[i];
        } else if (this.siteSetting[i].key == "why_book_with_us_box_6") {
          this.why_us_bwu_6 = this.siteSetting[i];
        } else if (this.siteSetting[i].key == "why_book_with_us_box_7") {
          this.why_us_bwu_7 = this.siteSetting[i];
        } else if (this.siteSetting[i].key == "why_book_with_us_box_8") {
          this.why_us_bwu_8 = this.siteSetting[i];
        } else if (this.siteSetting[i].key == "why_book_with_us_box_9") {
          this.why_us_bwu_9 = this.siteSetting[i];
        }
      }
    }
  },
};
</script>
