<template>
  <div class="global">
    <h3>
      <i class="fas fa-globe"></i> global
    </h3>
    <table>
      <tr>
        <th colspan="3">cases</th>
      </tr>
      <tr>
        <td class="icon-holder">
          <i class="fas fa-head-side-cough"></i>
        </td>
        <td>new</td>
        <td>+{{ global.NewConfirmed }}</td>
      </tr>
      <tr>
        <td class="icon-holder">
          <i class="fas fa-virus"></i>
        </td>
        <td>total</td>
        <td>{{ global.TotalConfirmed }}</td>
      </tr>

      <tr>
        <th colspan="3">recovered</th>
      </tr>

      <tr>
        <td class="icon-holder">
          <i class="fas fa-virus-slash"></i>
        </td>
        <td>new</td>
        <td>+{{ global.NewRecovered }}</td>
      </tr>

      <tr>
        <td class="icon-holder">
          <i class="fas fa-hand-sparkles"></i>
        </td>
        <td>total</td>
        <td>{{ global.TotalRecovered }}</td>
      </tr>

      <tr>
        <th colspan="3">deaths</th>
      </tr>
      <tr>
        <td class="icon-holder">
          <i class="fas fa-book-dead"></i>
        </td>
        <td>new</td>
        <td>+{{ global.NewDeaths }}</td>
      </tr>
      <tr>
        <td class="icon-holder">
          <i class="fas fa-skull-crossbones"></i>
        </td>
        <td>total</td>
        <td>{{ global.TotalDeaths }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "globalDashboard",
  props: {
    global: Object
  }
};
</script>

<style lang="scss" scoped>
$primary-color: #37d851;
$secondary-color: #570f83;

.global {
  background: #fff;
  border-radius: 15px;
  box-shadow: 0px 0px 5px darken($color: $primary-color, $amount: 2%);
  margin: 3vh auto 2rem;

  h3 {
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