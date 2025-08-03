<template>
  <div>
    <div class="duble-b">
      <div class="flight-radio-btns">
        <b-form-group>
          <div class="bv-no-focus-ring flight-search-detail">
            <b-form-radio-group
              v-model="type"
              :name="type"
              @input="typeChanged"
            >
              <b-form-radio name="some-radios" value="round" id="B"
              >Round Trip
              </b-form-radio
              >
              <b-form-radio name="some-radios" value="one"
              >One Way
              </b-form-radio
              >
              <b-form-radio name="some-radios" value="multi"
              >Multi City
              </b-form-radio
              >
            </b-form-radio-group>
          </div>
        </b-form-group>
      </div>

      <div class="flight-radio-btns nonstop">
        <b-form-group>
          <div class="bv-no-focus-ring mr-3">
            <b-form-checkbox v-model="data.nonStop" value="true">
              Non-Stop
            </b-form-checkbox>
          </div>
        </b-form-group>
        <b-form-group>
          <div class="bv-no-focus-ring">
            <b-form-checkbox v-model="data.flex" v-if="type != 'multi'">
              Flexible Search
            </b-form-checkbox>
          </div>
        </b-form-group>
      </div>
    </div>
    <div>
      <!-- below fields for round trip -->
      <div class="row search-fileds" v-if="type == 'round' || type == 'one'">
        <div class="col-lg-9">
          <div class="row">
            <div class="col-lg-6 mt-3" @click="$emit('scroll')">
              <b-autocomplete
                v-model="keywords.originLocationCode"
                @typing="simpleSuggestionList('originLocationCode')"
                placeholder="Origin"
                :data="locations.originLocationCode"
                :loading="fetchingLocations.originLocationCode"
                :disabled="fetchingLocations.originLocationCode"
                field="city"
                icon="airplane-takeoff"
                ref="destinationLocationCode"
                @select="
                  (option) => selectLocations('originLocationCode', option)
                "
                @focus="emptyLocations('originLocationCode')"
              >
                <template slot="empty"
                >No results for {{ keywords.originLocationCode }}
                </template
                >
                <template slot-scope="props">
                  <div class="media">
                    <div class="media-content">
                      {{
                      `${props.option.city} (${props.option.iata} - ${props.option.name}), ${props.option.country}`
                      }}
                    </div>
                  </div>
                </template>
              </b-autocomplete>
            </div>
            <div class="col-lg-6 mt-3" @click="$emit('scroll')">
              <b-autocomplete
                v-model="keywords.destinationLocationCode"
                @typing="simpleSuggestionList('destinationLocationCode')"
                placeholder="Destination"
                :data="locations.destinationLocationCode"
                :loading="fetchingLocations.destinationLocationCode"
                :disabled="fetchingLocations.destinationLocationCode"
                icon="airplane-landing"
                ref="destinationLocationCode"
                field="city"
                @select="
                  (option) => selectLocations('destinationLocationCode', option)
                "
                @focus="emptyLocations('destinationLocationCode')"
              >
                <template slot="empty"
                >No results for
                  {{ keywords.destinationLocationCode }}
                </template
                >
                <template slot-scope="props">
                  <div class="media">
                    <div class="media-content">
                      {{
                      `${props.option.city} (${props.option.iata} - ${props.option.name}), ${props.option.country}`
                      }}
                    </div>
                  </div>
                </template>
              </b-autocomplete>
            </div>
            <div class="col-lg-4 mt-1 col-xs-12 col-sm-12 col-md-9 mt-3">
              <!-- departure date calendar -->
              <date-range-picker
                opens="right"
                ref="picker"
                :timePicker="false"
                :single-date-picker="type == 'one' ? true : false"
                :minDate="this.dateToShow.minDate"
                :maxDate="this.dateToShow.maxDate"
                :showWeekNumbers="false"
                :showDropdowns="false"
                :ranges="false"
                :autoApply="true"
                v-model="dateToShow.dateRange"
                @update="this.handleDateRange"
              >
                <template class="date-range-picker" v-slot:input="picker">
<!--                  <mdicon name="Calendar-arrow-right"/>-->
                  <span class="mdi mdi-calendar-arrow-right"></span>
                  <b-form-input
                    :onclick="scrollFunction"
                    :value="calendarValue(picker.startDate)"
                    placeholder="Departure"
                    disabled
                    required
                  />
                </template>
              </date-range-picker>
            </div>
            <!-- arrival date calendar -->
            <div
              class="col-lg-4 col-xs-12 col-sm-12 col-md-9 mt-3"
              style="position: relative"
            >
              <date-range-picker
                opens="left"
                ref="picker"
                :timePicker="false"
                :minDate="this.dateToShow.minDate"
                :maxDate="this.dateToShow.maxDate"
                :showWeekNumbers="false"
                :showDropdowns="false"
                :ranges="false"
                :autoApply="true"
                v-model="dateToShow.dateRange"
                @update="this.handleDateRange"
                :disabled="type !== 'round'"
              >
                <template class="date-range-picker" v-slot:input="picker">
<!--                  <mdicon name="Calendar-arrow-left"/>-->
                  <span class="mdi mdi-calendar-arrow-left"></span>
                  <b-input
                    :value="
                      type == 'round'
                        ? calendarValue(picker.endDate)
                        : undefined
                    "
                    placeholder="Arrival"
                    disabled
                    required
                  >
                  </b-input>
                </template>
              </date-range-picker>
            </div>
            <div class="col-lg-4 col-xs-12 col-sm-12 col-md-9 mt-3">
              <b-dropdown ref="passengers" aria-role="list">
                <template #trigger>
                  <b-button class="btn btn-light arrow" style="width: 100%">
                    <small>
                      <span class="mdi mdi-human-male"></span>
                      {{ totalPassengers }}
                      <!-- Adult, -->
                    </small>
                    <span class="mdi mdi-seat-recline-normal ml-3"></span>
                    <small>
                      {{ travelClass(data.travelClass) }}
                    </small>
                  </b-button>
                </template>

                <div class="eqaul">
                  <b-form-select
                    v-model="data.includedAirline"
                    :options="allData.airlines"
                    value-field="iata"
                    text-field="name"
                  >
                    <b-form-select-option value="">ANY</b-form-select-option>
                  </b-form-select>
                  <div class="select-contain">
                    <select
                      class="select-contain-select"
                      v-model="data.travelClass"
                    >
                      <option selected value="ECONOMY">Economy</option>
                      <option value="PREMIUM_ECONOMY">Premium Economy</option>
                      <option value="BUSINESS">Business</option>
                      <option value="FIRST">First</option>
                    </select>
                  </div>
                </div>
                <div class="fix-adult">
                  <div class="sipn-row">
                    <div class="lable">
                      <h6>Adult</h6>
                    </div>
                    <div class="spin">
                      <b-form-spinbutton
                        id="sb-default"
                        min="1"
                        max="9"
                        placeholder="--"
                        v-model="data.adults"
                      ></b-form-spinbutton>
                    </div>
                  </div>
                  <div class="sipn-row">
                    <div class="lable">
                      <h6>Child</h6>
                    </div>
                    <div class="spin">
                      <b-form-spinbutton
                        id="sb-default"
                        min="0"
                        v-model="data.children"
                        placeholder="--"
                      ></b-form-spinbutton>
                    </div>
                  </div>
                  <div class="sipn-row">
                    <div class="lable">
                      <h6>Infant</h6>
                    </div>
                    <div class="spin">
                      <b-form-spinbutton
                        id="sb-default"
                        min="0"
                        v-model="data.infants"
                        placeholder="--"
                      ></b-form-spinbutton>
                    </div>
                  </div>
                </div>
              </b-dropdown>
            </div>
          </div>
        </div>
        <div class="col-lg-3 col-xs-12 col-sm-12 col-md-9 search-button">
          <button class="btn btn-light one-btn" @click="save">
            <span class="mr-1">Search for Flights</span>
            <i class="fa fa-chevron-right"></i>
          </button>
        </div>
      </div>
      <multiSearchForm v-else ref="multiCity" @redirect="redirect">
      </multiSearchForm>
    </div>
    <search-loading
      v-if="loading"
      :loadingParams="true"
      :params="data"
      title="We are Searching for the Best Flight Deals"
    >
    </search-loading>
  </div>
</template>
<script>
  import {mapState, mapMutations} from "vuex";
  import multiSearchForm from "@/components/multiSearchForm.vue";
  import DateRangePicker from "vue2-daterange-picker";
  import "vue2-daterange-picker/dist/vue2-daterange-picker.css";
  import searchLoading from "@/components/searchLoading";
  // import { mdiCalendarBlank } from '@mdi/js';

  export default {
    components: {
      multiSearchForm,
      DateRangePicker,
      searchLoading,
    },

    data() {
      let today = new Date();
      let yesterday = new Date();
      yesterday.setDate(today.getDate() - 1);
      return {
        searchParam: {},
        loading: false,
        // calendar data
        dateToShow: {
          departureDate: undefined,
          noDepartureDate: "Departure",
          returnDate: undefined,
          noReturnDate: "Arrival",
          dateRange: {
            startDate: undefined,
            endDate: undefined,
          },
          minDate: yesterday,
          maxDate: "2022-12-26 14:00:00",
          weekdays: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
          monthNames: [
            "Jan",
            "Feb",
            "Mar",
            "Apr",
            "May",
            "Jun",
            "Jul",
            "Aug",
            "Sep",
            "Oct",
            "Nov",
            "Dec",
          ],
        },

        activeTab: "",
        calendarData: {},
        selected: null,
        options: [
          {value: null, text: "Select Airline"},
          {value: "ALL", text: "Any class"},
          {value: "ECO", text: "Economy"},
          {value: "FIR", text: "First"},
          {value: "BUS", text: "Business"},
          {value: "PRE", text: "PREMIUM_ECONOMY"},
        ],
        loading: false,
        type: "round",
        data: {
          adults: 1,
          children: 0,
          infants: 0,
          locations: {},
          travelClass: "ECONOMY",
          includedAirline: "",
          flex: false,
          nonStop: false,
          returnDate: [],
        },
        keywords: {
          originLocationCode: "",
          destinationLocationCode: "",
        },
        oldKeywords: {
          originLocationCode: "",
          destinationLocationCode: "",
        },
        locations: {
          originLocationCode: [],
          destinationLocationCode: [],
        },
        fetchingLocations: {
          originLocationCode: false,
          destinationLocationCode: false,
        },
      };
    },

    watch: {
      calendarData: {
        handler(latest) {
          if (this.type === "round") {
            if (latest.dateRange.end) {
              let date = latest.dateRange.end.split("/");
              date = `${date[2]}-${this.$isoDate(date[1])}-${this.$isoDate(
                date[0]
              )}`;
              this.data.returnDate = new Date(date.replace(/-/g, "/"));
              this.$refs.calendar.hide(true);
              this.$refs.passengers.show(true);
              return;
            }
            if (latest.dateRange.start) {
              let date = latest.dateRange.start.split("/");
              date = `${date[2]}-${this.$isoDate(date[1])}-${this.$isoDate(
                date[0]
              )}`;
              this.data.departureDate = new Date(date.replace(/-/g, "/"));
              this.data.returnDate = null;
            }
          }
        },
        deep: true,
      },
    },

    beforeCreate() {
      let params = this.$store.state.forAll.searchParams;
      if (params && params.type !== "multi") {
        let start = params["departureDate"];
        start = `${start.getFullYear()}/${
          start.getMonth() + 1
        }/${start.getDate()}`;
        if (params.type === "round") {
          params["returnDate"] = params["returnDate"];
          let end = params["returnDate"];
          end = `${end.getFullYear()}/${end.getMonth() + 1}/${end.getDate()}`;
          this.$store.commit("form/setMarkedDateRange", {start, end});
        } else if (params.type === "one") {
          this.$store.commit("form/setMarkedDates", [start]);
        }
      }
    },

    created() {
      if (this.$route.name != "index") {
        if (this.searchParams) {
          if (this.searchParams.type !== "multi") {
            let data = {...this.searchParams};
            this.type = data.type;
            this.keywords.originLocationCode =
              data.locations.originLocationCode.city;
            this.keywords.destinationLocationCode =
              data.locations.destinationLocationCode.city;
            this.data = {...data};
            this.data.locations = {...data.locations};
          } else {
            this.type = "multi";
          }
        }
      }
      // console.log(JSON.parse(JSON.parse("{\"status\":\"Complete\",\"reportingSystem\":\"RAF\",\"timeStamp\":\"2022-01-10T11:52:00+00:00\",\"type\":\"Application\",\"errorCode\":\"WARN.RAF.APPLICATION\",\"instance\":\"raf-darhlp048.sabre.com-8080\",\"message\":\"{\\\"OTA_AirLowFareSearchRS\\\":{\\\"PricedItinCount\\\":0,\\\"BrandedOneWayItinCount\\\":0,\\\"SimpleOneWayItinCount\\\":0,\\\"DepartedItinCount\\\":0,\\\"SoldOutItinCount\\\":0,\\\"AvailableItinCount\\\":0,\\\"Version\\\":\\\"4.3.0\\\",\\\"Errors\\\":{\\\"Error\\\":[{\\\"Type\\\":\\\"IF2\\\",\\\"ShortText\\\":\\\"No complete journey can be built in IF2/ADVJR1.\\\",\\\"Code\\\":\\\"PROCESS\\\",\\\"content\\\":\\\"\\\"},{\\\"Type\\\":\\\"WORKERTHREAD\\\",\\\"ShortText\\\":\\\"4335643224154333116\\\",\\\"Code\\\":\\\"TRANSACTIONID\\\",\\\"MessageClass\\\":\\\"I\\\",\\\"content\\\":\\\"\\\"},{\\\"Type\\\":\\\"SERVER\\\",\\\"ShortText\\\":\\\"27041\\\",\\\"Code\\\":\\\"ASE032LPSPIL40C.IDM.SGDCPROD.SABRE.COM\\\",\\\"MessageClass\\\":\\\"I\\\",\\\"content\\\":\\\"\\\"},{\\\"Type\\\":\\\"DRE\\\",\\\"ShortText\\\":\\\"15863\\\",\\\"Code\\\":\\\"RULEID\\\",\\\"MessageClass\\\":\\\"I\\\",\\\"content\\\":\\\"\\\"},{\\\"Type\\\":\\\"DEFAULT\\\",\\\"ShortText\\\":\\\"28096\\\",\\\"Code\\\":\\\"RULEID\\\",\\\"MessageClass\\\":\\\"I\\\",\\\"content\\\":\\\"\\\"},{\\\"Type\\\":\\\"SCHEDULES\\\",\\\"ShortText\\\":\\\"NO FLIGHT SCHEDULES FOR QUALIFIERS USED\\\",\\\"Code\\\":\\\"MSG\\\",\\\"MessageClass\\\":\\\"I\\\",\\\"content\\\":\\\"\\\"},{\\\"Type\\\":\\\"ERR\\\",\\\"ShortText\\\":\\\"Error during Processing\\\",\\\"Code\\\":\\\"ERR\\\",\\\"content\\\":\\\"\\\"}]}},\\\"Links\\\":[{\\\"rel\\\":\\\"self\\\",\\\"href\\\":\\\"https://api.havail.sabre.com/v4.3.0/shop/flights?mode=live\\\"},{\\\"rel\\\":\\\"linkTemplate\\\",\\\"href\\\":\\\"https://api.havail.sabre.com/<version>/shop/flights?mode=<mode>&limit=<limit>&offset=<offset>&enabletagging=<enabletagging>\\\"}]}\"}").message))
    },

    computed: {
      ...mapState("forAll", ["searchParams", "airports", "airlines"]),
      ...mapState("data", ["allData"]),
      ...mapState("form", ["markedDateRange", "markedDates"]),

      totalPassengers() {
        let totalPassengers = this.data.adults;
        if (this.data.children) {
          totalPassengers += this.data.children;
        }
        if (this.data.infants) {
          totalPassengers += this.data.infants;
        }
        return totalPassengers;
      },

      minReturnDate() {
        let startDate = new Date();
        if (this.data.departureDate) {
          return this.data.departureDate;
        } else {
          return startDate;
        }
      },

      maxDepartDate() {
        if (this.data.returnDate) {
          return this.data.returnDate;
        } else {
          return;
        }
      },
    },

    methods: {
      ...mapMutations("forAll", ["setSearchParams"]),
      ...mapMutations("flights", ["setFlexResponse", "setAjaxResponse"]),

      typeChanged: function () {
        this.data.departureDate = null;
        this.data.returnDate = null;
      },

      scrollFunction() {
        if (
          document.body.scrollTop > screen.height - 400 ||
          document.documentElement.scrollTop > screen.height - 400
        ) {
          // document.getElementById("navbar").style.top = "0";
          console.log("aaa");
        } else {
          console.log("bbb");
          // document.getElementById("navbar").style.top = "-50px";
        }
      },

      travelClass(classType) {
        switch (classType) {
          case "ECONOMY":
            return "ECO";
            break;
          case "FIRST":
            return "FIR";
            break;
          case "BUSINESS":
            return "BUS";
            break;
          case "PREMIUM_ECONOMY":
            return "PRE";
            break;
          default:
            return "ALL";
            break;
        }
      },

      emptyLocations(type) {
        this.data.locations[type] = null;
        this.keywords[type] = null;
      },

      dayClicled(date, key) {
        if (date && date.length > 1 && typeof date == "object") {
          this.data.departureDate = date[0];
          this.data.returnDate = date[1];
        } else {
          if (key == "departureDate") {
            this.data.departureDate = new Date(date.replace(/-/g, "/"));
          }
          if (key == "returnDate") {
            this.data.returnDate = new Date(date.replace(/-/g, "/"));
          }
        }
      },

      handleDateRange() {
        this.data.departureDate = this.dateToShow.dateRange.startDate;
        // this.dateToShow.departureDate=this.convertDate(values[0])
        // alert(this.convertDate(values[0]))
        if (this.type == "round") {
          this.data.returnDate = this.dateToShow.dateRange.endDate;
        }
        // this.dateToShow.returnDate=this.convertDate(values[1])
      },
      calendarValue(value) {
        return value ? this.convertDate(value) : "";
      },

      // handleDateRange(values){
      //   this.data.departureDate = values[0];
      //   this.dateToShow.departureDate=this.convertDate(values[0])
      //   // alert(this.convertDate(values[0]))
      //   this.data.returnDate = values[1];
      //   this.dateToShow.returnDate=this.convertDate(values[1])
      // },
      //
      convertDate(str) {
        var date = new Date(str),
          weekday = date.getDay(),
          mnth = date.getMonth(),
          day = ("0" + date.getDate()).slice(-2);
        return [
          this.dateToShow.weekdays[weekday] + ",",
          this.dateToShow.monthNames[mnth],
          day + ",",
          date.getFullYear(),
        ].join(" ");
      },

      selectLocations(type, option) {
        this.data.locations[type] = option;
        // console.log(this.data.locations);
        if (type === "destinationLocationCode") {
          // this.$refs.calendar.show(true);
        } else {
          this.$refs.destinationLocationCode.focus();
        }
      },

      simpleSuggestionList(type) {
        this.data.locations[type] = null;
        if (this.timer !== null) {
          clearTimeout(this.timer);
        }
        this.timer = setTimeout(async () => {
          let keyword = this.keywords[type].toLowerCase();
          if (!keyword.length || keyword.length < 2) {
            this.locations[type] = [];
            return;
          }
          this.fetchingLocations[type] = true;

          if (
            this.locations[type].length < 1 ||
            this.oldKeywords[type].length > keyword.length
          ) {
            this.locations[type] = this.allData.airports.filter((x) =>
              x.iata.toLowerCase().includes(keyword)
            );
            if (this.locations[type].length < 1) {
              this.locations[type] = this.allData.airports.filter((x) =>
                x.name.toLowerCase().includes(keyword)
              );
            }
            if (this.locations[type].length < 1) {
              this.locations[type] = this.allData.airports.filter(
                (x) =>
                  x.city.toLowerCase().includes(keyword) ||
                  x.country.toLowerCase().includes(keyword)
              );
            }
          } else {
            this.locations[type] = this.locations[type].filter((x) =>
              x.iata.toLowerCase().includes(keyword)
            );
            if (this.locations[type] < 1) {
              this.locations[type] = this.locations[type].filter((x) =>
                x.name.toLowerCase().includes(keyword)
              );
            }
            if (this.locations[type] < 1) {
              this.locations[type] = this.locations[type].filter(
                (x) =>
                  x.city.toLowerCase().includes(keyword) ||
                  x.country.toLowerCase().includes(keyword)
              );
            }
          }

          if (
            this.locations[type].length < 1 ||
            this.oldKeywords[type].length > keyword.length
          ) {
            this.locations[type] = this.allData.airports.filter(
              (x) =>
                x.name.toLowerCase().includes(keyword) ||
                x.city.toLowerCase().includes(keyword) ||
                x.country.toLowerCase().includes(keyword) ||
                x.iata.toLowerCase().includes(keyword)
            );
          } else {
            this.locations[type] = this.locations[type].filter(
              (x) =>
                x.name.toLowerCase().includes(keyword) ||
                x.city.toLowerCase().includes(keyword) ||
                x.country.toLowerCase().includes(keyword) ||
                x.iata.toLowerCase().includes(keyword)
            );
          }
          this.oldKeywords[type] = keyword;
          this.fetchingLocations[type] = false;
        }, 100);
      },

      mount() {
        if (this.loadFares) {
          this.loading = true;
          if (!this.params) {
            return this.redirect();
          }
          let data = {...this.params};
          if (this.params.type !== "multi") {
            let soapData = {destinations: []};
            soapData.destinations[0] = {};
            soapData.destinations[0]["departureLocation"] =
              data.locations.originLocationCode.iata;
            soapData.destinations[0]["arrivalLocation"] =
              data.locations.destinationLocationCode.iata;
            if (data["returnDate"]) {
              soapData.destinations[1] = {};
              soapData.destinations[1]["departureLocation"] =
                soapData.destinations[0]["arrivalLocation"];
              soapData.destinations[1]["arrivalLocation"] =
                soapData.destinations[0]["departureLocation"];
              let date = new Date(data["returnDate"]);
              soapData.destinations[1]["date"] = data[
                "returnDate"
                ] = `${date.getFullYear()}-${this.$isoDate(
                date.getMonth() + 1
              )}-${this.$isoDate(date.getDate())}`;
            }
            let date = new Date(data["departureDate"]);
            soapData.destinations[0][
              "date"
              ] = `${date.getFullYear()}-${this.$isoDate(
              date.getMonth() + 1
            )}-${this.$isoDate(date.getDate())}`;
            soapData.nonStop = data.nonStop;
            soapData.travelClass = data.travelClass;
            soapData.includedAirline = data.includedAirline;
            soapData["passengers"] = _.pick(data, [
              "adults",
              "children",
              "infants",
            ]);
            soapData["flex"] = data.flex || false;
            this.ajax(soapData);
          } else {
            let soapData = {destinations: []};
            for (var index in data.destinations) {
              soapData["destinations"][index] = {};
              soapData["destinations"][index]["departureLocation"] =
                data.destinations[index].locations.originLocationCode.iata;
              soapData["destinations"][index]["arrivalLocation"] =
                data.destinations[index].locations.destinationLocationCode.iata;
              let date = new Date(data.destinations[index]["departureDate"]);
              date = `${date.getFullYear()}-${this.$isoDate(
                date.getMonth() + 1
              )}-${this.$isoDate(date.getDate())}`;
              soapData["destinations"][index].date = date;
            }
            soapData.nonStop = data.nonStop;
            soapData.travelClass = data.travelClass;
            soapData.includedAirline = data.includedAirline;
            soapData["passengers"] = _.pick(data, [
              "adults",
              "children",
              "infants",
            ]);
            this.ajax(soapData);
          }
        } else {
          this.setLoadFares(true);
        }
      },

      redirect() {
        this.$router.push("/");
      },
      // reformateType(data) {
      //   if (data == 'round') {
      //     return 'ROUND_TRIP'
      //   } else if (data == 'one') {
      //     return 'ONE_WAY'
      //   } else if (data == 'multi') {
      //     return 'MULTI_DIRECTIONAL'
      //   } else {
      //     return 'ROUND_TRIP'
      //   }
      // },
      // convertApiDate(dataDate) {
      //   let date = new Date(dataDate);
      //   let year = date.getFullYear();
      //   let month = date.getMonth() + 1;
      //   let dt = date.getDate();
      //
      //   if (dt < 10) {
      //     dt = '0' + dt;
      //   }
      //   if (month < 10) {
      //     month = '0' + month;
      //   }
      //
      //   let newdate = year + '-' + month + '-' + dt;
      //   return newdate;
      // },
      // reformateData(thisData) {
      //   let data = thisData;
      //   // console.log(data)
      //   return {
      //     trip: this.reformateType(data.type),
      //     origion_name:
      //       data.locations.originLocationCode.city + " (" + data.locations.originLocationCode.iata + " - " +
      //       data.locations.originLocationCode.name + "), " + data.locations.originLocationCode.country,
      //     origion_code: data.locations.originLocationCode.iata,
      //     distination_name:
      //       data.locations.destinationLocationCode.city + " (" + data.locations.destinationLocationCode.iata + " - " +
      //       data.locations.destinationLocationCode.name + "), " + data.locations.destinationLocationCode.country,
      //     distination_code: data.locations.destinationLocationCode.iata,
      //     depart_date: this.convertApiDate(data.departureDate),
      //     return_date: this.convertApiDate(data.returnDate),
      //     adult: data.adults,
      //     child: data.children ? data.children : null,
      //     infant: data.infants ? data.infants : null,
      //     cabin_class: data.travelClass == '' ? 'ECONOMY' : data.travelClass,
      //   }
      //   // console.log(data.travelClass)
      // },
      //
      // ajax(params) {
      //
      //   // console.log(this.searchParams)
      //   // if (process.env.NODE_ENV != "production" && process.env.CACHE == "true") {
      //   //   if (this.params.flex) {
      //   //     let flightResponse = JSON.parse(
      //   //       localStorage.getItem("flexSearchResponse")
      //   //     );
      //   //     // console.log(flightResponse),
      //   //     this.setFlexResponse(flightResponse);
      //   //   } else {
      //   //     this.setAjaxResponse({
      //   //       response: flightResponse,
      //   //       airlinesByKey: this.airlinesByKey,
      //   //     });
      //   //   }
      //   //   this.loading = false;
      //   // } else {
      //   // localStorage.removeItem('searchResponse')
      //   this.loading = true
      //   // alert('run')
      //   this.$api({
      //     method: "post",
      //     url: "flight_search_api",
      //     data: this.reformateData(params),
      //   })
      //     .then(({data}) => {
      //       this.searchData = data
      //       localStorage.setItem("searchResponse", JSON.stringify(data));
      //       this.setAjaxResponse({
      //         response: data,
      //         airlinesByKey: this.airlinesByKey,
      //       });
      //       // console.log(this.searchData)
      //       // console.log('params',this.params)
      //       if (
      //         process.env.NODE_ENV != "production" &&
      //         process.env.CACHE == "true"
      //       ) {
      //         localStorage.setItem("flexSearchResponse", JSON.stringify(data));
      //       }
      //       // if (this.params.flex) {
      //       //   this.setFlexResponse(data);
      //       // } else {
      //       //   this.setFlexResponse({
      //       //     response: data,
      //       //     airlinesByKey: this.airlinesByKey,
      //       //   });
      //       // }
      //       this.notFoundError = false;
      //       this.timer = setTimeout(() => {
      //         this.$bvModal.show("search_expired");
      //       }, 3600000);
      //     })
      //     .catch((err) => {
      //       this.notFoundError = true;
      //       console.log("error", err);
      //       let data = err.response.data;
      //       if (data.messages) {
      //         for (var message of data.messages) {
      //           this.$bvToast.toast(
      //             `Code: ${message.code}, Message ${message.text}`,
      //             {
      //               title: "AATourism",
      //               variant: "danger",
      //               solid: true,
      //               toaster: "b-toaster-top-center",
      //             }
      //           );
      //         }
      //       }
      //     })
      //     .finally(
      //       () => {
      //         if (this.$route.name != "flights") {
      //           // alert(this.$route.name)
      //           if (params.flex == true) {
      //             // this.setFlexResponse(null);
      //             this.$router.push("flights");
      //             // this.loading = false;
      //           }
      //           if (params.flex == false) {
      //             this.$router.push("flights");
      //             // this.loading = false;
      //           }
      //           if (params.flex == undefined) {
      //             this.$router.push("flights");
      //             // this.loading = false;
      //           }
      //         }
      //         // this.loading = false;
      //         // if (this.$route.name === "flights") {
      //         //   this.$emit("search");
      //         // } else {
      //         //   if (params.flex == true) {
      //         //     this.setFlexResponse(null);
      //         //     this.$router.push("flights");
      //         //   }
      //         //   if (params.flex == false) {
      //         //     this.$router.push("flights");
      //         //   }
      //         //   if (params.flex == undefined) {
      //         //     this.$router.push("flights");
      //         //   }
      //         // }
      //         // this.redirect(params)
      //       }
      //       //  {
      //       //       if(this.$store.state.loading){
      //       // this.$store.commit("setLoading")
      //       //       }
      //       // }
      //     );
      //   // }
      // },
      save() {
        // alert('tested')
        if (
          !this.data.locations.originLocationCode ||
          !this.data.locations.destinationLocationCode
        ) {
          return this.errorMessage();
        }
        if (this.type === "one") {
          if (!this.data.departureDate) {
            return this.errorMessage();
          }
        }
        if (this.type === "round") {
          if (!this.data.departureDate || !this.data.returnDate) {
            return this.errorMessage();
          }
        }
        this.data.type = this.type;

        let totalPassengers = this.data.adults;
        if (this.data.children === 0) {
          delete this.data.children;
        } else {
          totalPassengers += this.data.children;
        }
        if (this.data.infants === 0) {
          delete this.data.infants;
        } else {
          totalPassengers += this.data.children;
        }
        // if (totalPassengers >= 10) {
        //   return this.$bvToast.toast(
        //     "Total number of passengers should be less than or equal to 9.",
        //     {
        //       title: "AATourism!",
        //       variant: "danger",
        //       toaster: "b-toaster-bottom-right",
        //       solid: true,
        //     }
        //   );
        // }
        // if (this.data.infants > this.data.adults) {
        //   return this.$bvToast.toast(
        //     "Infant passengers should be less than or equal to adult passengers",
        //     {
        //       title: "AATourism!",
        //       variant: "danger",
        //       toaster: "b-toaster-bottom-right",
        //       solid: true,
        //     }
        //   );
        // }
        // localStorage.setItem("offerType", "offer");
        this.redirect(this.data)
      },
      redirect(data) {
        data.nonStop = this.data.nonStop;
        localStorage.setItem("offerParams", JSON.stringify(data));
        localStorage.setItem("searchParams", JSON.stringify(data));
        if (this.$route.name === "flights") {
          this.$emit("search");
        }
        else {
          if (data.flex == true) {
            this.$router.push("flights");
          }
          if (data.flex == false) {
            this.$router.push("flights");
          }
          if (data.flex == undefined) {
            this.$router.push("flights");
          }
        }
      },

      errorMessage() {
        this.$bvToast.toast("Provided data is not valid", {
          title: "AATourism!",
          variant: "danger",
          toaster: "b-toaster-top-center",
          solid: true,
        });
      },
    },
  };

  // function
</script>
