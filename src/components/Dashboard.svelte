<script>
  import DashboardInfo from "./DashboardInfo.svelte";
  import LineChart from "./LineChart.svelte";
  import Text from "./Text.svelte";
  import dataLocal from "../data/data";

  export let data;

  let dataset = [];
  let datasetBackup = [];

  for (const date in data) {
    const dateObject = new Date(date);
    dataset.push({ date: dateObject, price: data[date] });
  }

  for (const date in dataLocal) {
    const dateObject = new Date(date);
    datasetBackup.push({ date: dateObject, price: dataLocal[date] });
  }
</script>

<div>
  <DashboardInfo data={dataset.length !== 0 ? dataset : datasetBackup} />
  <LineChart data={dataset.length !== 0 ? dataset : datasetBackup} />
  <Text />
</div>

<style>
  div {
    flex: 1;
  }
</style>
