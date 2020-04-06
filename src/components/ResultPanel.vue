<template>
  <div class="result-panel">
    <div class="country">
      <img class="flag" v-bind:src="country.selectedCountry.flag" alt="flag" width="32" />
      <h3>{{ country.selectedCountry.Country }}</h3>
    </div>
    <table>
      <tr>
        <th colspan="3">cases</th>
      </tr>
      <tr>
        <td class="icon-holder">
          <i class="fas fa-head-side-cough"></i>
        </td>
        <td>new</td>
        <td>+{{ country.selectedCountry.NewConfirmed }}</td>
      </tr>

      <tr>
        <td class="icon-holder">
          <i class="fas fa-virus"></i>
        </td>
        <td>total</td>
        <td>{{ country.selectedCountry.TotalConfirmed }}</td>
      </tr>

      <tr>
        <th colspan="3">recovered</th>
      </tr>

      <tr>
        <td class="icon-holder">
          <i class="fas fa-virus-slash"></i>
        </td>
        <td>new</td>
        <td>+{{ country.selectedCountry.NewRecovered }}</td>
      </tr>

      <tr>
        <td class="icon-holder">
          <i class="fas fa-hand-sparkles"></i>
        </td>
        <td>total</td>
        <td>{{ country.selectedCountry.TotalRecovered }}</td>
      </tr>

      <tr>
        <th colspan="3">deaths</th>
      </tr>
      <tr>
        <td class="icon-holder">
          <i class="fas fa-book-dead"></i>
        </td>
        <td>new</td>
        <td>+{{ country.selectedCountry.NewDeaths }}</td>
      </tr>
      <tr>
        <td class="icon-holder">
          <i class="fas fa-skull-crossbones"></i>
        </td>
        <td>total</td>
        <td>{{ country.selectedCountry.TotalDeaths }}</td>
      </tr>

      <tr>
        <th class="last-update" colspan="3">last updated</th>
      </tr>
      <tr>
        <td class="icon-holder">
          <i class="far fa-calendar-alt"></i>
        </td>
        <td>date</td>
        <td>{{ country.lastUpdated.date }}</td>
      </tr>

      <tr>
        <td class="icon-holder">
          <i class="fas fa-clock"></i>
        </td>
        <td>time</td>
        <td>{{ country.lastUpdated.time }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "resultPanel",
  props: {
    country: Object
  }
};
</script>

<style lang="scss" scoped>
$primary-color: #37d851;
$secondary-color: #570f83;

.result-panel {
  background: #fff;
  border-radius: 15px;
  box-shadow: 0px 0px 5px darken($color: $primary-color, $amount: 2%);
  margin: 3vh auto 2rem;

  .country {
    padding: 1rem;
    text-align: center;
    text-transform: uppercase;
    border-bottom: 3px solid $primary-color;
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
</style>
