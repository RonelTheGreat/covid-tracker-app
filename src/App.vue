<template>
  <div id="app">
    <h2>covid-19 tracker</h2>
    <div v-if="isFetching" class="overlay">
      <app-loading />
    </div>
    <search-bar v-bind:countries="countries" v-on:get-country="getCountry" />
    <result-panel v-if="hasResult" v-bind:country="{selectedCountry, lastUpdated}" />
    <global-dashboard v-if="!isFetching" v-bind:global="global" />
    <app-footer />
  </div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";
import ResultPanel from "./components/ResultPanel.vue";
import GlobalDashboard from "./components/GlobalDashboard.vue";
import AppLoading from "./components/AppLoading.vue";
import AppFooter from "./components/AppFooter.vue";

export default {
  name: "App",
  components: {
    SearchBar,
    ResultPanel,
    GlobalDashboard,
    AppLoading,
    AppFooter
  },
  data() {
    return {
      isFetching: false,
      isReady: false,
      countries: [],
      global: {},
      lastUpdated: {
        time: "",
        date: ""
      },
      hasResult: false,
      selectedCountry: {},
      strMonths: [
        "Jan.",
        "Feb.",
        "March",
        "April",
        "May",
        "June",
        "July",
        "Aug.",
        "Sept.",
        "Oct.",
        "Nov.",
        "Dec."
      ]
    };
  },
  mounted() {
    this.fetchAvailableCountries();
  },
  methods: {
    getCountry(received) {
      let selected = this.countries.filter(
        country => country.CountryCode === received
      )[0];

      selected.NewConfirmed = this.formatNumber(selected.NewConfirmed);
      selected.TotalConfirmed = this.formatNumber(selected.TotalConfirmed);
      selected.NewRecovered = this.formatNumber(selected.NewRecovered);
      selected.TotalRecovered = this.formatNumber(selected.TotalRecovered);
      selected.NewDeaths = this.formatNumber(selected.NewDeaths);
      selected.TotalDeaths = this.formatNumber(selected.TotalDeaths);

      this.selectedCountry = selected;
      this.selectedCountry.flag = `https://www.countryflags.io/${this.selectedCountry.CountryCode.toLowerCase()}/flat/32.png`;
      this.selectedCountry.date = this.lastUpdated.date;
      this.selectedCountry.time = this.lastUpdated.time;

      this.hasResult = true;
    },
    fetchAvailableCountries() {
      this.isFetching = true;
      fetch("https://api.covid19api.com/summary", { method: "GET" })
        .then(res => {
          return res.json();
        })
        .then(data => {
          this.countries = data.Countries;
          this.global = data.Global;

          let {
            NewConfirmed,
            TotalConfirmed,
            NewRecovered,
            TotalRecovered,
            NewDeaths,
            TotalDeaths
          } = this.global;

          this.global.NewConfirmed = this.formatNumber(NewConfirmed);
          this.global.TotalConfirmed = this.formatNumber(TotalConfirmed);
          this.global.NewRecovered = this.formatNumber(NewRecovered);
          this.global.TotalRecovered = this.formatNumber(TotalRecovered);
          this.global.NewDeaths = this.formatNumber(NewDeaths);
          this.global.TotalDeaths = this.formatNumber(TotalDeaths);
          const refDate = data.Date;

          // format date and time
          const date = new Date(refDate);
          const lastUpdatedDate = `${
            this.strMonths[date.getMonth()]
          } ${date.getDate()}, ${date.getFullYear()}`;

          const time = this.formatTime(date);

          this.lastUpdated.date = lastUpdatedDate;
          this.lastUpdated.time = time;
          this.isFetching = false;
        });
    },
    formatNumber(num) {
      return num.toString().replace(/(\d)(?=(\d{3})+(?!\d))/g, "$1, ");
    },
    formatTime(date) {
      // get hour and minute
      let hours = date.getHours();
      let minutes = date.getMinutes();

      // get time of the day, PM or AM
      // if hour is greater than 12, then it is PM else it is AM
      let ampm = hours >= 12 ? "PM" : "AM";

      // get hour
      hours = hours % 12;
      hours = hours ? hours : 12;

      // if minute less than 10, add 0 to the front (e.g 09, 08 etc.)
      minutes = `${minutes < 10 ? "0" + minutes : minutes}`;

      // store the formatted time
      let time = `${hours}:${minutes} ${ampm}`;

      return time;
    }
  }
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Montserrat&display=swap");
$primary-color: #37d851;
$secondary-color: #570f83;

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-size: 18px;
  font-family: "Montserrat", sans-serif;
  color: #570f83;
  background: url("./assets/bg-right-with-corona.svg") no-repeat;
  background-attachment: fixed;
  background-size: cover;
  background-blend-mode: overlay;
}

#app {
  max-width: 100vw;
  max-height: 100vh;
  padding: 2.4rem;

  h2 {
    text-align: center;
    text-transform: uppercase;
    margin: 0;
    padding: 0;
  }

  .overlay {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.2);
    z-index: 9999;
  }
}

table {
  border-collapse: collapse;
  width: 100%;
  th {
    text-transform: uppercase;
    text-align: center;
    background: rgba(55, 216, 81, 0.3);
    padding: 0.8rem;
  }
  td {
    padding: 0.6rem;
    position: relative;
    text-transform: capitalize;
  }

  td:first-child,
  td:nth-child(2) {
    border-right: 1px solid rgba(55, 216, 81, 0.2);
  }

  td:last-child {
    font-weight: bolder;
    text-align: center;
    letter-spacing: 1px;
  }

  th:first-child {
    width: 1rem;
  }

  .icon-holder {
    width: 1%;
    text-align: center;
  }
}

@media screen and (min-width: 1024px) {
  body {
    background-size: contain;
    background-position-x: right;
  }
  #app {
    height: 100vh;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: 15% 3rem 2fr 4rem;
    column-gap: 5%;
    padding: 2rem;
    grid-template-areas:
      "h ."
      "sb g"
      "rp g"
      "f g";
    h2 {
      grid-area: h;
      align-self: center;
    }

    .search-parent {
      grid-area: sb;
      margin: 0 auto;
      width: 60%;

      .search-bar {
        margin: 0 auto;
      }
    }

    .result-panel {
      grid-area: rp;
      margin: 2rem auto;
      min-width: 60%;
      align-self: flex-start;
    }

    .global {
      grid-area: g;
      align-self: flex-start;
      margin: 0 5%;
    }

    footer {
      grid-area: f;

      p {
        display: none;
      }
      img {
        max-width: 32px;
      }
    }
  }
}
</style>
