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
                <h1>Get In Touch</h1>
                <!-- <span class="mdi mdi-airplane mdi-rotate-90"></span> -->
              </div>
              <h5>Home/Contact Us</h5>
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
      <div class="contact-content pt-6">
        <!-- <div class="cheap-deal">
        <h3>International / Domestic Flight Deals</h3>
        <h6>“The world is a book, and those who do not travel read only one page” Book a lavish flight to your dream destination. Fly with AA Travel & tours anywhere in the world, at a competitive price.</h6>
        <small>
          Read more
          <span class="mdi mdi-chevron-down"></span>
        </small>
      </div> -->
        <div class="contact-main">
            <div class="row">
                <div class="col-lg-4">
                    <div class="contect-detail-box">
                        <img
                        src="../static/address.svg"
                        alt=""
                        />
                        <h5>Address:</h5>
                        <p>{{address.value}}</p>
                    </div>
                </div>
                <div class="col-lg-4">
                    <div class="contect-detail-box">
                        <img
                        src="../static/phone.svg"
                        alt=""
                        />
                        <h5>Phone:</h5>
                        <p>{{phoneNo.value}}</p>
                    </div>
                </div>
                <div class="col-lg-4">
                    <div class="contect-detail-box">
                        <img
                        src="../static/email.svg"
                        alt=""
                        />
                        <h5>Email us:</h5>
                        <p><a :href="'mailto:'+email.value">{{email.value}}</a></p>
                    </div>
                </div>
            </div>
        </div>
        
      </div>
      <div class="contact-form">
        <div class="contact-main">
            <div class="row">
                <div class="col-lg-6">
                    <div class="text-section">
                    <h3>{{contactPage.name}}</h3>
                    <h6>
                        {{contactPage.value}}
                    </h6>
                    <p v-html="contactPage.description">
                    </p>
                    </div>
                </div>
                <div class="col-lg-6">
                    <div class="text-section">
                    <div class="row">
                        <div class="col-lg-6">
                          <b-form-group class="form-label color-dark-2">
                            <b-form-input
                              data-vv-name="name"
                              placeholder="Enter Your Name"
                              v-validate="'required|max:190'"
                              class="form-control-rounded"
                              type="text"
                              v-model="data.contact.name"
                              id="name"
                              :state="errors.has('name') ? false : null"
                            ></b-form-input>
                            <b-tooltip
                              v-if="errors.has('name')"
                              :show="true"
                              triggers="focus"
                              target="name"
                              placement="bottom"
                              variant="danger"
                              >{{ errors.first("name") }}</b-tooltip
                            >
                          </b-form-group>
                        </div>
                        <div class="col-lg-6">
                          <b-form-group class="form-label color-dark-2">
                            <b-form-input
                              data-vv-name="email"
                              placeholder="Email Address"
                              v-validate="'required|max:190|email'"
                              class="form-control-rounded"
                              type="text"
                              v-model="data.contact.email"
                              id="email"
                              :state="errors.has('email') ? false : null"
                            ></b-form-input>
                            <b-tooltip
                              v-if="errors.has('email')"
                              :show="true"
                              triggers="focus"
                              target="email"
                              placement="bottom"
                              variant="danger"
                              >{{ errors.first("email") }}</b-tooltip
                            >
                          </b-form-group>
                        </div>
                        <div class="col-lg-6">
                          <b-form-group class="form-label color-dark-2">
                            <b-form-input
                              data-vv-name="phone_no"
                              placeholder="Phone No."
                              v-validate="'max:190'"
                              class="form-control-rounded"
                              type="text"
                              v-model="data.contact.phone"
                              id="phone_no"
                              :state="errors.has('phone_no') ? false : null"
                            ></b-form-input>
                            <b-tooltip
                              v-if="errors.has('phone_no')"
                              :show="true"
                              triggers="focus"
                              target="phone_no"
                              placement="bottom"
                              variant="danger"
                              >{{ errors.first("phone_no") }}</b-tooltip
                            >
                          </b-form-group>
                        </div>
                        <div class="col-lg-6">
                          <b-form-group class="form-label color-dark-2">
                            <b-form-input
                              data-vv-name="subject"
                              placeholder="Subject"
                              v-validate="'required|max:190'"
                              class="form-control-rounded"
                              type="text"
                              v-model="data.contact.subject"
                              id="subject"
                              :state="errors.has('subject') ? false : null"
                            ></b-form-input>
                            <b-tooltip
                              v-if="errors.has('subject')"
                              :show="true"
                              triggers="focus"
                              target="subject"
                              placement="bottom"
                              variant="danger"
                              >{{ errors.first("subject") }}</b-tooltip
                            >
                          </b-form-group>
                        </div>
                        <div class="col-lg-12">
                          <b-form-group class="form-label color-dark-2">
                            <b-form-textarea
                              data-vv-name="comments"
                              placeholder="Enter Your Comments"
                              v-validate="'required|max:190'"
                              class="form-control-rounded"
                              rows="5"
                              type="text"
                              v-model="data.contact.comments"
                              id="comments"
                              :state="errors.has('comments') ? false : null"
                            ></b-form-textarea>
                            <b-tooltip
                              v-if="errors.has('comments')"
                              :show="true"
                              triggers="focus"
                              target="comments"
                              placement="bottom"
                              variant="danger"
                              >{{ errors.first("comments") }}</b-tooltip
                            >
                          </b-form-group>
                        </div>
                        <div class="col-lg-12">
                          <button @click.prevent="contactUs" class="btn btn-light">
                            <span>Submit Comment</span>
                            <i class="fa fa-chevron-right"></i>
                          </button>
                        </div>
                    </div>
                    </div>
                </div>
            </div>
        </div>
      </div>
      <div class="Contact-map">
        <div class="map">
          <iframe width="100%" height="400" style="border:0" loading="lazy" allowfullscreen 
src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d217897.55247430058!2d72.94921391894748!3d31.423788302099965!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x392242a895a55ca9%3A0xdec58f88932671c6!2sFaisalabad%2C%20Punjab%2C%20Pakistan!5e0!3m2!1sen!2s!4v1630000448066!5m2!1sen!2s" ></iframe>
          
        </div>
      </div>
    </div>
    <!-- flight-detail-section -->
    <!-- <b-sidebar
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
                :to="{ name: 'flightDetail'}"
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
    </b-sidebar> -->
    <!-- flight-detail-section -->
  </div>
</template>
<script>
import { mapGetters } from "vuex";

export default {
  data() {
    return {
      value: "250",
      data: {
        contact: {},
      },
      phoneNo: "",
      faxNo: "",
      email: "",
      siteUrl: "",
      address: "",
      contactPage: "",
    };
  },
  computed: {
    ...mapGetters({
      siteSetting: "siteSetting/getSetting",
    }),
  },
  created(){
    if (this.siteSetting == undefined) {
      this.$api.get("/setting").then(({ data }) => {
        this.$store.commit("siteSetting/setSetting", data);
        for (var i = 0; i < data.data.length; i++) {
          if (data.data[i].key == "phoneNo") {
            this.phoneNo = data.data[i];
          // } else if (data.data[i].key == "fax") {
          //   this.faxNo = data.data[i];
          } else if (data.data[i].key == "email") {
            this.email = data.data[i];
          // } else if (data.data[i].key == "siteUrl") {
          //   this.siteUrl = data.data[i];
          } else if (data.data[i].key == "address") {
            this.address = data.data[i];
          // } else if (data.data[i].key == "footerDescription") {
          //   this.footerDescription = data.data[i];
          } else if (data.data[i].key == "contactPage") {
            this.contactPage = data.data[i];
          // } else if (data.data[i].key == "contact_us_email") {
          //   this.contactUsEmail = data.data[i].value;
          // } else if (data.data[i].key == "facebook_url") {
          //   this.facebook_url = data.data[i];
          // } else if (data.data[i].key == "linkedin_url") {
          //   this.linkedin_url = data.data[i];
          // } else if (data.data[i].key == "twitter_url") {
          //   this.twitter_url = data.data[i];
          // } else if (data.data[i].key == "instagram_url") {
          //   this.instagram_url = data.data[i];
          }
        }
      });
    } else {
      for (var i = 0; i < this.siteSetting.length; i++) {
        if (this.siteSetting[i].key == "phoneNo") {
          this.phoneNo = this.siteSetting[i];
        // } else if (this.siteSetting[i].key == "fax") {
        //   this.faxNo = this.siteSetting[i];
        } else if (this.siteSetting[i].key == "email") {
          this.email = this.siteSetting[i];
        // } else if (this.siteSetting[i].key == "siteUrl") {
        //   this.siteUrl = this.siteSetting[i];
        } else if (this.siteSetting[i].key == "address") {
          this.address = this.siteSetting[i];
        // } else if (this.siteSetting[i].key == "facebook_url") {
        //   this.facebook_url = this.siteSetting[i];
        // } else if (this.siteSetting[i].key == "linkedin_url") {
        //   this.linkedin_url = this.siteSetting[i];
        // } else if (this.siteSetting[i].key == "twitter_url") {
        //   this.twitter_url = this.siteSetting[i];
        // } else if (this.siteSetting[i].key == "instagram_url") {
        //   this.instagram_url = this.siteSetting[i];
        } else if (this.siteSetting[i].key == "contactPage") {
          this.contactPage = this.siteSetting[i];
        // } else if (this.siteSetting[i].key == "contact_us_email") {
        //   this.contactUsEmail = this.siteSetting[i].value;
        }
      }
    }
  },
  methods:{
    contactUs() {
      this.$validator.validate().then((result) => {
        if (result) {
          this.$api({
            method: "post",
            url: "contact",
            data: {
              name: this.data.contact.name,
              email: this.data.contact.email,
              message: this.data.contact.comments,
              subject: this.data.contact.subject,
              phone: this.data.contact.phone,
            },
          })
            .then(({ data }) => {
              // console.log(data);
              if (data) {
                
                this.$root.$bvToast.toast(
                  `Your message has successfully sent`,
                  {
                    title: "AA Travel & Tourism!",
                    variant: "success",
                    solid: true,
                    toaster: "b-toaster-top-center",
                  }
                );
              }
            })
            .catch((err) => {
              if (err) {
                this.$root.$bvToast.toast(`Provided data is in valid`, {
                  title: "AA Travel & Tourism!",
                  variant: "danger",
                  solid: true,
                  toaster: "b-toaster-top-center",
                });
              }
              // console.log(err);
              // console.log(err.response);
            })
            .finally(() => {
              
              // console.log("finally");
            });
        }
      });
    },
  }
};
</script>
