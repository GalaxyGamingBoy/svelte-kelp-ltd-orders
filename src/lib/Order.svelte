<script lang="ts">
  export let order;

  function calculateProgress(status) {
    switch (status) {
      case 'In progress':
        return 50;
      case 'Done':
        return 100;
      default:
        return 0;
    }
  }

  function statusText(status) {
    switch (status) {
      case 'In progress':
        return 'Kelp LTD is currently working on your order.';
      case 'Done':
        return (
          'Kelp LTD has completed your order. Please pick it up at ' +
          order.fields['Where would like to receive your order?']
        );
      default:
        return 'Kelp LTD is currenty processing your order. Check back later.';
    }
  }
</script>

<div>
  <div class="card">
    <div class="card-header">Order #{order.id}</div>
    <div class="card-body">
      <h5 class="card-title">
        <b>IGN:</b>
        {order.fields['What is your in-game username?']}
      </h5>
      <p class="card-text">
        <b>Order Status: </b>{statusText(order.fields.Status)}
      </p>
      <div>
        <table class="table table-striped">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Block Count</th>
              <th scope="col">Location</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <th scope="row">{order.id}</th>
              <td>{order.fields['How many kelp blocks do you need?']}</td>
              <td>{order.fields['Where would like to receive your order?']}</td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="progress" role="progressbar" aria-label="order-progressbar">
        <div
          class="progress-bar"
          style="width: {calculateProgress(order.fields.Status)}%"
        />
      </div>
    </div>
  </div>
</div>
