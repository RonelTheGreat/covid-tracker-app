<template>
  <div class="search-parent">
    <form v-on:submit.stop class="search-bar">
      <input v-model.trim="countryName" type="text" placeholder="Search for a country" />
      <i class="fas fa-search"></i>
    </form>

    <ul v-show="searchResult.length >= 1">
      <h3 class="tag">
        <i class="fas fa-search"></i>
        Search Result:
        <span>{{searchResult.length}} out of {{countries.length}}</span>
      </h3>
      <li
        v-on:click="getCountry(country.code)"
        v-for="(country, index) in searchResult"
        v-bind:key="index"
      >{{country.name}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "SearchBar",
  props: {
    countries: Array
  },
  data() {
    return {
      countryName: "",
      searchResult: []
    };
  },

  watch: {
    countryName: function() {
      if (this.countryName.length >= 1) {
        // iterate through countries
        // and filter according to input value
        const result = this.countries
          .map(country => {
            return {
              name: country.Country,
              slug: country.Slug,
              code: country.CountryCode
            };
          })
          .filter(country => {
            return country.name
              .toLowerCase()
              .startsWith(this.countryName.toLowerCase());
          });

        this.searchResult = result;
      } else {
        this.searchResult = [];
      }
    }
  },
  methods: {
    getCountry(countryCode) {
      this.$emit("get-country", countryCode);
      this.searchResult = [];
      this.countryName = "";
    }
  }
};
</script>

<style lang="scss" scoped>
$primary-color: #37d851;
$secondary-color: #570f83;

.search-bar {
  display: grid;
  grid-template-columns: 1fr 2rem;
  border: 3px solid $primary-color;
  padding: 0.2rem 0.4rem;
  border-radius: 10px;
  margin: 9vw auto 1vw;
  background: #fff;
  align-items: center;
  justify-items: center;

  input {
    text-transform: uppercase;
    border: none;
    padding: 0.4rem 0.2rem;
    font-size: 1rem;
    outline: none;
    width: 100%;
    height: 100%;
    color: $secondary-color;
  }

  input::placeholder {
    color: #37c44cad;
    text-transform: capitalize;
  }

  i {
    padding: 0.4rem 0.2rem;
    color: #37c44cad;
  }
}

.search-parent {
  ul {
    list-style-type: none;
    display: block;
    position: relative;
    background: #fff;
    font-size: 0.9rem;
    border-radius: 10px;
    box-shadow: 0px 0px 5px darken($color: $primary-color, $amount: 2%);
    margin: 2vh auto;
    max-height: 200px;
    overflow-y: auto;
    z-index: 9999;

    h3 {
      padding: 1rem;
      position: sticky;
      top: 0;
      background: #fff;
      border-radius: 10px;

      span {
        padding-left: 0.5rem;
        font-size: 0.9rem;
        color: lighten($color: $secondary-color, $amount: 10);
      }
    }

    li {
      padding: 0.6rem 1rem;
    }

    li:hover {
      background: rgba(55, 216, 81, 0.2);
      cursor: pointer;
    }
  }
}
</style>
