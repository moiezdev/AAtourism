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
                <h1>News</h1>
                <!-- <span class="mdi mdi-airplane mdi-rotate-90"></span> -->
              </div>
              <h5>Home/news</h5>
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
      <div class="deals pt-2">
        <!-- <div class="cheap-deal">
        <h3>International / Domestic Flight Deals</h3>
        <h6>“The world is a book, and those who do not travel read only one page” Book a lavish flight to your dream destination. Fly with AA Travel & tours anywhere in the world, at a competitive price.</h6>
        <small>
          Read more
          <span class="mdi mdi-chevron-down"></span>
        </small>
      </div> -->
        <div class="news-box">
          <div class="row">
                <div class="col-lg-9">
                  <div class="row">
                      <div v-if="is_expired_news(news.expiry_date) == false" v-for="(news, index) in allNews" class="col-lg-4">
                          <div class="news-detail-box">
                              <div v-bind:style="{ 'background-image': 'url(https://fseaatourism.aatourism.ca/assets/' + news.image + ')'}" class="europe-united">
                              
                              </div>
                              <div class="text-area">
                              <h6>
                                  <span class="mdi mdi-calendar"></span>
                                  {{format(news.created_at)}}
                              </h6>
                              <div class="news-detail-rate">
                                  <nuxt-link
                                      :to="{
                                      name: 'news-id',
                                      params: {id: news.id}
                                      }"
                                  > 
                                  <div class="left">
                                  <h5>
                                      {{news.title}}
                                  </h5>
                                  </div>
                                  </nuxt-link>
                              </div>
                              </div>
                          </div>
                      </div>
                  </div>
                  <div v-if="all_data.current_page" class="pagination-box">
                    <div class="pagination:container">
                      <div class="pagination:number arrow" @click="get_news('/news?page='+all_data.prev_page_url.substr(all_data.prev_page_url.length - 1))">
                        <svg width="18" height="18">
                          <use xlink:href="#left" />
                        </svg>
                      </div>
                      
                      <div v-if="all_data.current_page != 1" @click="get_news('/news?page='+parseInt(all_data.current_page-1))" class="pagination:number">{{all_data.current_page-1}}</div>
                      <div class="pagination:number pagination:active">{{all_data.current_page}}</div>
                      <div @click="get_news('/news?page='+all_data.last_page)" v-if="all_data.last_page != all_data.current_page" class="pagination:number">{{all_data.last_page}}</div>
                      <!-- <div class="pagination:number">2</div>
                      <div class="pagination:number pagination:active">3</div>
                      <div class="pagination:number">4</div>
                      <div class="pagination:number">540</div> -->
                      
                      <div class="pagination:number arrow" @click="get_news('/news?page='+all_data.next_page_url.substr(all_data.next_page_url.length - 1))">
                        <svg width="18" height="18">
                          <use xlink:href="#right" />
                        </svg>
                      </div>
                    </div>

                    <svg class="hide">
                      <symbol id="left" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path></symbol>
                      <symbol id="right" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path></symbol>
                    </svg>
                  </div>
                </div>
                <div class="col-lg-3">
                    <div class="news-detail-box">
                    <div class="news-side-area">
                        <div class="news-detail-rate">
                            <div class="left">
                                <h5>
                                News Categories
                                </h5>
                            </div>
                        </div>
                        <div class="news-detail-rate">
                            <!-- <nuxt-link
                                :to="{
                                    name: 'news-details',
                                }"
                                >  -->
                            <div class="left">
                                <h6 @click="filter_cat(cat)" v-for="(cat, index) in newsCat">
                                    <span class="mdi mdi-arrow-right-drop-circle-outline"></span>
                                    {{cat}}
                                </h6>
                            </div>
                            <!-- </nuxt-link> -->
                        </div>
                    </div>
                    </div>
                </div>
          </div>
        </div>
        
      </div>
      <div class="your-best-deal">
        <div class="heading">
          <h4>Your best deal in no time!</h4>
        </div>
        <div class="container best-deal-outer">
          <div class="row">
            <div class="col-lg-3 best-deal-box">
              <img src="../../static/USP_icon_1.png" width="120px" alt />
              <h6>
                Compare
                <br />800+ Airlines
              </h6>
            </div>
            <div class="col-lg-3 best-deal-box">
              <img src="../../static/USP_icon_2.png" width="120px" alt />
              <h6>
                Easy and
                <br />fast booking
              </h6>
            </div>
            <div class="col-lg-3 best-deal-box">
              <img src="../../static/USP_icon_3.png" width="120px" alt />
              <h6>
                English speaking
                <br />customer service
              </h6>
            </div>
            <div class="col-lg-3 best-deal-box">
              <img src="../../static/USP_icon_4.png" width="120px" alt />
              <h6>
                AA Travel & Tourism is
                <br />a member of IATA
              </h6>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- flight-detail-section -->
<!--     <b-sidebar
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
                :to="{ name: 'flightDetail"
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
import moment from "moment";

export default {
  data() {
    return {
      value: "250",
      allNews: [],
      newsCat: ['All'],
      all_data: {}

    };
  },
  computed: {
    ...mapGetters({
      siteNews: "news/getNews",
    }),
  },
  created(){
    if (this.siteNews == undefined) {
      this.get_news('/news');
    } else {
      this.allNews = this.siteNews;
      for (var i = 0; i < this.allNews.length; i++) {
          if(!this.newsCat.includes(this.allNews[i].category_name)){
            this.newsCat.push(this.allNews[i].category_name);
          }
        }
    }
    if(this.$route.params.category){
      this.filter_cat(this.$route.params.category);
    }
  },
  methods: {
    format(date) {
      return moment(date).format("DD-MM-YYYY");
    },
    is_expired_news(expiry_date){
      if(expiry_date == null) return false;
      return !moment().isBefore(expiry_date);
    },
    filter_cat(cat_name){
      const vm = this;
      if(cat_name == 'All'){
        this.allNews = this.siteNews;
      }else{
        this.allNews = [];
        this.siteNews.forEach(function(news){
          if(news.category_name == cat_name){
            vm.allNews.push(news);
          }
        });
      }
    },
    get_news(url){
      if(url == null) return; 
      this.$api.get(url).then(({ data }) => {
        this.all_data = data;
        this.allNews = [];
        this.$store.commit("news/setNews", data);
        for (var i = 0; i < data.data.length; i++) {
          this.allNews.push(data.data[i]);
          if(!this.newsCat.includes(data.data[i].category_name)){
            this.newsCat.push(data.data[i].category_name);
          }
          
        }
        // this.allNews = this.allNews.slice(0, 2);
      });
    }
  }
};
</script>
