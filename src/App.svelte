<script lang="ts">
  import Order from './lib/Order.svelte';
  const noError = 'No Error';

  let orders = [];
  let ign = '';
  let error = noError;

  const apiURL = 'https://kelp-ltd-orders-production.up.railway.app';
  const orderURL = apiURL + '/orders';

  function fetchData() {
    let orderIGNURL;

    if (ign !== '' && ign) {
      error = noError;
      fetch(orderURL + `/${ign}`)
        .then((res) => res.json())
        .then((data) => {
          orders = data;
        });
    } else {
      error = 'Please enter a valid IGN';
    }
  }
</script>

<main class="m-5">
  <div class="card">
    <div class="card-header">Order Lookup</div>
    <div class="card-body">
      <h5 class="card-title">Got an order?</h5>
      <p class="card-text">
        Don't hesitate to look it up. Just enter your IGN.
      </p>
      <div class="input-group mb-3">
        <span class="input-group-text" id="ign">IGN</span>
        <input
          type="text"
          class="form-control"
          placeholder="i.e. GalaxyGamingBoy"
          aria-label="ign"
          aria-describedby="ign"
          bind:value={ign}
        />
      </div>

      <a href="#lookup" class="btn btn-primary" on:click={fetchData}>Lookup</a>
    </div>
  </div>

  <br />
  <div class="alert alert-danger" role="alert">{error}</div>
  <br />

  {#each orders as order}
    <Order {order} />
    <br />
  {/each}
</main>
