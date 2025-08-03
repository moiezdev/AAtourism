<template>
  <div class="container-fluid flight-list-body">
    <div class="height-38"></div>
    <div class="flights-page">

      <div class="flights-heading">
        <div class="container pb-3 pt-1">
          <div class="flights-modify-section">
            <div class="left">
              <div class="flight-top-section">
                <h1>{{pakage_detail != null ? pakage_detail.name : ''}}</h1>
              </div>
              <h5
                v-if="pakage_detail">{{pakage_detail.package_country.region}}/{{pakage_detail.package_country.name}}</h5>
            </div>
            <div>
              <div class="right">
                <router-link :to="{name: 'pkg-booknow'}" class="pkgbook-button-outer">
                  <button class="btn btn-light">
                    <span>Book Now</span>
                  </button>
                </router-link>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="packages-deals pt-2">
        <div v-if="pakage_detail != undefined" class="hotel-deals">
          <div class="row">
            <div :key="index" v-for="(day, index) in pakage_detail.days" class="blog-list">
              <div class="blog-list-entry">
                <div class="row">
                  <div class="col-lg-4">
                    <div class="blog-list-top">
                      <img :src="day.image ? `${$config.ASSET_URL}${day.image}` : ''">
                    </div>
                  </div>
                  <div class="col-lg-8">
                    <div class="package-detail-text">
                      <h4 class="blog-list-title">
                        <span>{{day.location}}</span>
                      </h4>
                      <div class="blog-list-text">
                        <p v-html="day.description"></p>
                      </div>
                      <div class="package-detail-text">
                        <h4 class="blog-list-title">
                          <div class="days">DAY {{index+1}}</div>
                        </h4>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div v-if="pakage_detail != undefined && pakage_detail.extra" class="row">
            <div class="col-lg-12">
              <div v-html="pakage_detail.extra"></div>
            </div>
          </div>
          <div class="row">
            <div class="col-lg-2 pkgbook-button">
              <button @click="$router.back()" class="btn btn-light">
                <span>Back</span>
              </button>
            </div>
            <div class="col-lg-8"></div>
            <div class="col-lg-2 pkgbook-button">
              <router-link :to="{name: 'pkg-booknow'}" class="pkgbook-button-outer">
                <button class="btn btn-light">
                  <span>Book Now</span>
                </button>
              </router-link>
            </div>
          </div>
        </div>
      </div>
      <div class="your-best-deal">
        <div class="heading">
          <h4>TOUR GALLERY</h4>
        </div>
        <div class="container gallery-images">
          <div v-if="pakage_detail != undefined" class="row">
            <div  :key="index" v-for="(gal_image_data, index) in pakage_detail.images" class="col-lg-4 gallery-images-box">
              <img @click="openGallery(index)" :src="gal_image_data.image ? `${$config.ASSET_URL}${gal_image_data.image}` : ''" width="100%" alt />
            </div>
          </div>
        </div>
      </div>
      <LightBox
        v-if="pakage_detail != undefined"
        ref="lightbox"
        :show-caption="true"
        :show-light-box="false"
        :media="create_media_src()">
      </LightBox>
    </div>
  </div>
</template>
<script>
  import { mapGetters } from "vuex";
  import LightBox from 'vue-image-lightbox'
  require('vue-image-lightbox/dist/vue-image-lightbox.min.css')

  export default {
    data() {
      return {
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
        pakage_detail: null,
        showlightbox: false
      };
    },
    components: {
      LightBox,
    },
    computed: {
      ...mapGetters({
        PakageDetails: "pakages/getPakageDetail",
      }),
    },
    head() {
    return {
      title: this.pakage_detail && this.pakage_detail.name?this.pakage_detail.name:'Package Name',
      meta: [
        { hid: "keyword", name: "keyword", content: this.pakage_detail && this.pakage_detail.keyword?this.pakage_detail.keyword:'' },
        {
          hid: "description",
          name: "description",
          content: this.pakage_detail && this.pakage_detail.description?this.pakage_detail.description:'Description',
        },
      ],
    };
  },
    created(){
      this.$api.get(`/package/${this.$route.params.id}?related=true`).then(({ data }) => {

        this.$store.commit("pakages/setPakageDetail", data);
        this.pakage_detail = data;
        console.log('pakage_detail',this.pakage_detail)
      });
    },
    methods:{
      create_media_src() {
        var all_images = [];
        this.PakageDetails.images.forEach(function(val){
          all_images.push(
            {
              thumb: `${'https://fseaatourism.aatourism.ca/assets/'+val.image}`,
              src: `${'https://fseaatourism.aatourism.ca/assets/'+val.image}`
            }
          )
        });
        return all_images;
      },
      openGallery(index) {
        this.$refs.lightbox.showImage(index)
      }
    }
  };
</script>
