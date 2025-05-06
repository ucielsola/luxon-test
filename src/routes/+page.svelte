<script>
  import { DateTime } from "luxon";

  const userTimeZone = Intl.DateTimeFormat().resolvedOptions().timeZone;

  let date = $state(DateTime.now().toISODate());
  let time = $state("12:00");
  let timeZone = $state("Europe/Berlin");

  const timeZones = [
    "Europe/Berlin",
    "America/New_York",
    "America/Argentina/Buenos_Aires",
    "Asia/Tokyo",
    "Europe/London",
    "Australia/Sydney",
  ];

  let utc = $derived(
    DateTime.fromISO(`${date}T${time}`, { zone: timeZone }).toUTC()
  );

  let ba = $derived(utc.setZone("America/Argentina/Buenos_Aires"));
  let ny = $derived(utc.setZone("America/New_York"));
  let local = $derived(utc.setZone(userTimeZone));
  let payload = $derived({
    date: utc.toISO(),
    timezone: timeZone,
  });
</script>

<div class="container">
  <h2>Timezone test with Luxon</h2>

  <div class="blocks">
    <div class="block">
      <div class="label">Buenos Aires</div>
      <div class="value">{ba.toFormat("dd/MM/yyyy HH:mm ZZZZ")}</div>
    </div>
    <div class="block">
      <div class="label">New York</div>
      <div class="value">{ny.toFormat("dd/MM/yyyy HH:mm ZZZZ")}</div>
    </div>
    <div class="block">
      <div class="label">Your Location ({userTimeZone})</div>
      <div class="value">{local.toFormat("dd/MM/yyyy HH:mm ZZZZ")}</div>
    </div>
  </div>

  <div class="block">
    <div class="label">Payload to save:</div>
    <pre class="json-preview">{JSON.stringify(payload, null, 2)}</pre>
  </div>

  <hr />

  <form class="form">
    <label>
      Date:
      <input type="date" bind:value={date} />
    </label>

    <label>
      Time:
      <input type="time" bind:value={time} />
    </label>

    <label>
      Timezone:
      <select bind:value={timeZone}>
        {#each timeZones as tz}
          <option value={tz}>{tz}</option>
        {/each}
      </select>
    </label>
  </form>
</div>

<style>
  hr {
    margin-block: 3rem;
  }

  .container {
    max-width: 700px;
    margin: 2rem auto;
    font-family: sans-serif;
  }

  .blocks {
    display: flex;
    gap: 1rem;
    justify-content: space-between;
    margin-bottom: 2rem;
  }

  .block {
    flex: 1;
    border: 1px solid #ccc;
    border-radius: 6px;
    padding: 1rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  .label {
    font-size: 0.9rem;
    color: #555;
    margin-bottom: 0.4rem;
  }

  .value {
    font-weight: bold;
    font-size: 1.2rem;
  }

  form.form {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    align-items: flex-end;
  }

  label {
    display: flex;
    flex-direction: column;
    font-size: 0.9rem;
    flex: 1;
  }

  .json-preview {
    background: #f9f9f9;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 1rem;
    font-family: monospace;
    white-space: pre-wrap;
    word-break: break-word;
  }
</style>
