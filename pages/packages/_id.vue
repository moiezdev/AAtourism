<template>
  <div class="container-fluid flight-list-body">
    <div class="height-38"></div>
    <div class="flights-page">
      
      <div class="flights-heading">
        <div class="container pb-3 pt-1">
          <div class="flights-modify-section">
            <div class="left">
              <div class="flight-top-section">
                <h1>{{country.name}}</h1>
              </div>
              <h5>{{country.region}}</h5>
            </div>
            <div>
              <div class="right">
                
                  <button @click="$router.back()" class="btn btn-primary">Back</button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="deals pt-2">
        <div class="hotel-deals">
          <div class="row" v-if="allPackages.length > 0">
            <div  :key="index" v-for="(pakage, index) in allPackages" class="col-lg-4 col-md-6">
              <div class="hotel-deal-box">
                <div v-bind:style="{ 'background-image': 'url(https://fseaatourism.aatourism.ca/assets/' + pakage.image + ')'}" class="europe-united">
                  <!-- <h3>{{pakage.name}}</h3> -->
                </div>
                <div class="text-area">
                  <h2 v-html="pakage.description.length > 150 ? pakage.description.substring(0,150)+'...' : pakage.description">
                  </h2>
                  <div class="hotel-deal-rate">
                    <div class="left">
                      <h5>
                        {{pakage.day != '' ? pakage.day+' Days': ''}} {{pakage.night != '' ? pakage.night+' Nights': ''}}
                        <span class="mdi mdi-chevron-double-right"></span>
                      </h5>
                    </div>
                    <div class="right">
                      <h5>
                        <small>From</small>
                        <span>C$</span> {{pakage.price}}
                      </h5>
                    </div>
                  </div>
                  <div class="hotel-deal-rate">
                    <nuxt-link
                        :to="{
                          name: 'pakagedetails-id',
                          params: { id: pakage.id }
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
            </div>
            <div v-if="allPackages.length <= 0 && loading == false" class="no_pakage col-lg-12 col-md-12">
              <img src="../../static/nopackage.png" alt />
              <h3>No Pakage Found</h3>
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
  </div>
</template>
<script>
import { mapGetters } from "vuex";

export default {
  data() {
    return {
      loading: false,
      value: "250",
      regions: [
        'Asia',
        'Middle East',
        'Africa',
        'North America',
        'South America',
        'Antaractica',
        'Europe',
        'Australia'
      ],
      allPackages:[],
      country: {}
    };
  },
  computed: {
    ...mapGetters({
      pakages: "pakages/getPakages",
      pakageCountry: "pakages/getPakageCountry",
    }),
  },
  created(){
    this.loading = true;
    this.$nextTick(() => {
      this.$nuxt.$loading.start();
    })
    if (typeof this.$route.params.id == "number") {
    this.$api.get(`/package`).then(({ data }) => {
      this.$store.commit("pakages/setPakages", data);
      var allPackages = []
      for (var i = 0; i < data.data.length; i++) {
        if (data.data[i].package_country_id == this.$route.params.id) {
          allPackages.push(data.data[i]);
        }
      }
      this.allPackages = allPackages;
      this.$nuxt.$loading.finish();
      this.loading = false;
    });
    this.$api.get(`/packagecountry/${this.$route.params.id}`).then(({ data }) => {
      
      this.$store.commit("pakages/setPakageCountry", data);
      this.country = data;
    });
  }
  else{
    this.$api.get(`/package`).then(({ data }) => {
      this.$store.commit("pakages/setPakages", data);
      var allPackages = []
      for (var i = 0; i < data.data.length; i++) {
        if (data.data[i].package_country && this.convertSmall(data.data[i].package_country.region) == this.$route.params.id) {
          allPackages.push(data.data[i]);
        }
      }
      this.allPackages = allPackages;
      this.$nuxt.$loading.finish();
      this.loading = false;
    });
    this.$api.get(`/packagecountry`).then(({ data }) => {
      
      this.$store.commit("pakages/setPakageCountry", data);
      this.country = data;
    });
  }
  },
  methods: {
    convertSmall(string){
      return string.toLowerCase()
    }
  },
};
</script>
<style type="text/css">
  .no_pakage{
    text-align: center;
    color: gray;
    opacity: 0.6;
  }
</style>
