<script>
  import { DateTime } from "luxon";
  import { writable } from "svelte/store";

  let selectedDate = $state(DateTime.now().toISODate());
  let dt = $derived(DateTime.fromISO(selectedDate + "T12:00:00Z"));
  let bsAs = $derived(dt.setZone("America/Argentina/Buenos_Aires"));
  let berlin = $derived(dt.setZone("Europe/Berlin"));
</script>

<div class="container">
  <h3><a href="https://moment.github.io/luxon/">Luxon</a></h3>
  <input class="date-input" type="date" bind:value={selectedDate} />

  <div class="boxes">
    <div class="box">
      <div class="label">Buenos Aires</div>
      <div class="time">{bsAs.toFormat("dd/MM/yyyy HH:mm ZZZZ")}</div>
    </div>

    <div class="box">
      <div class="label">Berlín</div>
      <div class="time">{berlin.toFormat("dd/MM/yyyy HH:mm ZZZZ")}</div>
    </div>
  </div>

  <a href="https://github.com/ucielsola/luxon-test">code</a>
</div>

<style>
  .container {
    display: flex;
    gap: 1rem;
    align-items: center;
    margin: 2rem auto;
    padding: 1rem;
    font-family: sans-serif;
  }

  .date-input {
    display: block;
    padding: 0.5rem;
    font-size: 1rem;
    border: 1px solid #ccc;
    border-radius: 4px;
  }

  .boxes {
    display: flex;
    justify-content: space-between;
    gap: 1rem;
  }

  .box {
    flex: 1;
    border: 1px solid #ccc;
    border-radius: 8px;
    padding: 1rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  .label {
    font-size: 0.9rem;
    color: #666;
    margin-bottom: 0.5rem;
  }

  .time {
    font-size: 1.2rem;
    font-weight: bold;
  }
</style>
