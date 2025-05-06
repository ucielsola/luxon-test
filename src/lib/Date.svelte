<script>
  let selectedDate = $state(new Date().toISOString().slice(0, 10));

  function formatInTimeZone(dateStr, timeZone) {
    const date = new Date(dateStr + "T12:00:00Z");

    const formatter = new Intl.DateTimeFormat("default", {
      timeZone,
      year: "numeric",
      month: "2-digit",
      day: "2-digit",
      hour: "2-digit",
      minute: "2-digit",
      timeZoneName: "short",
    });

    return formatter.format(date);
  }

  let ba = $derived(
    formatInTimeZone(selectedDate, "America/Argentina/Buenos_Aires")
  );
  let berlin = $derived(formatInTimeZone(selectedDate, "Europe/Berlin"));
</script>

<div class="container">
  <h3>Browser Date api</h3>
  <input class="date-input" type="date" bind:value={selectedDate} />

  <div class="boxes">
    <div class="box">
      <div class="label">Buenos Aires</div>
      <div class="time">{ba}</div>
    </div>

    <div class="box">
      <div class="label">Berlín</div>
      <div class="time">{berlin}</div>
    </div>
  </div>
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
