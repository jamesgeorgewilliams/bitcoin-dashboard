<script>
  import * as d3 from "d3";

  export let data;

  const yAccessor = (d) => d.price;
  const monthHigh = d3
    .max(data, yAccessor)
    .toLocaleString("en", { minimumFractionDigits: 2 });

  const monthLow = d3
    .min(data, yAccessor)
    .toLocaleString("en", { minimumFractionDigits: 2 });

  const currentPrice = yAccessor(data[data.length - 1]).toLocaleString("en", {
    minimumFractionDigits: 2,
  });

  const percentageChange = Number(
    (
      ((yAccessor(data[data.length - 1]) - yAccessor(data[data.length - 2])) /
        yAccessor(data[data.length - 2])) *
      100
    ).toFixed(2)
  );

  let isNegative = false;
  if (percentageChange >= 0) {
    isNegative = !isNegative;
  }
</script>

<div class="info">
  <div class="info__upper">
    <div class="info__upper-left">
      <span class="header__left-heading">
        <svg
          version="1.1"
          id="Capa_1"
          xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink"
          x="0px"
          y="0px"
          height="32"
          width="32"
          viewBox="0 0 512.009 512.009"
          style="enable-background:new 0 0 512.009 512.009;"
          xml:space="preserve">
          <g>
            <path
              style="fill:#FFAF46;"
              d="M266.611,8.733C130.051,2.861,14.596,108.81,8.725,245.361s100.077,252.015,236.628,257.886
        c136.551,5.871,252.015-100.069,257.886-236.628c0,0,0,0,0-0.009C509.102,130.059,403.162,14.604,266.611,8.733z M300.158,91.119
        l-8.833,32.975L300.158,91.119z M356.089,212.13c-9.754,36.423-47.192,58.039-83.607,48.285c-0.009,0-0.017,0-0.026-0.009
        l-82.429-22.094l98.916,26.506c36.423,9.754,58.039,47.192,48.285,83.607c0,0.009,0,0.017-0.009,0.026l0,0
        c-9.754,36.423-47.192,58.039-83.607,48.285c-0.009,0-0.017,0-0.026-0.009l-32.975-8.833l-8.833,32.966l8.833-32.966
        l-49.497-13.253l-8.833,32.975l8.901-33.009l-16.488-4.421l-32.966-8.833l32.966,8.833l35.347-131.891l35.339-131.883
        l-32.975-8.824l32.975,8.841l16.487,4.412l8.833-32.966l-8.833,32.966l65.941,17.674
        C344.227,138.269,365.843,175.707,356.089,212.13L356.089,212.13z"
            />
            <path
              style="fill:#FFAF46;"
              d="M307.813,128.514l-65.941-17.674l0,0l-16.487-4.412l-35.339,131.883l82.429,22.094
        c36.423,9.763,73.852-11.854,83.615-48.276S344.235,138.277,307.813,128.514z"
            />
            <path
              style="fill:#FFAF46;"
              d="M171.185,374.607L171.185,374.607l49.497,13.253l32.975,8.833
        c36.414,9.771,73.861-11.837,83.624-48.251c0-0.009,0-0.017,0.009-0.026l0,0c9.771-36.414-11.837-73.861-48.251-83.624
        c-0.009,0-0.017,0-0.026-0.009l-98.968-26.472l-35.347,131.891L171.185,374.607z"
            />
          </g>
          <g>
            <path
              style="fill:#231F20;"
              d="M256.251,512.002c-3.746,0-7.493-0.077-11.265-0.239C103.724,505.67-5.851,386.204,0.242,244.942
        c2.927-67.802,32.651-131.661,82.642-177.556c104.19-95.597,266.147-88.633,361.744,15.549s88.633,266.138-15.549,361.735
        C382.006,488.082,320.281,512.13,256.251,512.002z M255.739,17.036C123.771,17.181,16.9,124.282,17.046,256.241
        c0.068,59.737,22.504,117.281,62.895,161.299c89.23,97.227,240.391,103.704,337.618,14.473
        c46.68-42.849,74.441-102.484,77.155-165.788l0,0c5.658-131.849-96.638-243.31-228.487-248.968
        C262.745,17.104,259.229,17.036,255.739,17.036z"
            />
            <path
              style="fill:#231F20;"
              d="M364.367,214.34c10.958-40.98-13.373-83.078-54.344-94.044l-8.244-2.21l6.622-24.748
        c1.195-4.557-1.528-9.225-6.085-10.42c-4.531-1.186-9.165,1.493-10.403,6.008l-6.622,24.748l-32.975-8.867l6.631-24.748
        c1.195-4.557-1.528-9.225-6.085-10.42c-4.532-1.186-9.165,1.493-10.403,6.008l-6.622,24.748l-41.219-11.043
        c-4.514-1.34-9.268,1.229-10.616,5.743c-1.34,4.514,1.229,9.268,5.743,10.616c0.145,0.043,0.299,0.085,0.444,0.119l24.748,6.631
        l-66.274,247.295l-24.748-6.631c-4.557-1.195-9.225,1.528-10.42,6.085c-1.186,4.531,1.493,9.165,6.008,10.403l41.219,11.043
        l-6.631,24.748c-1.212,4.549,1.485,9.225,6.033,10.445c0.717,0.196,1.459,0.299,2.21,0.299c3.866,0,7.245-2.594,8.244-6.332
        l6.622-24.748l32.975,8.833l-6.622,24.748c-1.212,4.549,1.485,9.225,6.033,10.445c0.717,0.196,1.459,0.299,2.21,0.299
        c3.866,0,7.245-2.594,8.244-6.332l6.622-24.748l24.748,6.622c19.671,5.325,40.655,2.56,58.278-7.681
        c36.713-21.181,49.3-68.109,28.128-104.813c-5.803-10.053-13.808-18.664-23.417-25.175
        C338.885,259.134,357.659,239.259,364.367,214.34z M328.994,346.223c-8.534,31.866-41.296,50.785-73.161,42.243h-0.009
        l-90.673-24.296l30.918-115.404l90.639,24.287C318.574,281.604,337.494,314.349,328.994,346.223z M274.693,252.162l-74.177-19.875
        l30.901-115.404l74.185,19.884c31.806,8.756,50.495,41.645,41.731,73.451C338.663,241.717,306.302,260.397,274.693,252.162
        L274.693,252.162z"
            />
          </g>
        </svg>
        Bitcoin price
      </span>
    </div>
    <div class="info__upper-right">
      <p>USD</p>
    </div>
  </div>
  <div class="info__lower">
    <div class="info__lower-left">
      <span class="header__left-heading-price">${currentPrice}</span>
      <span class={isNegative ? "positive" : "negative"}>
        {isNegative ? "+" : ""}{percentageChange}%</span
      >
    </div>
    <div class="info__lower-right">
      <div>
        <label for="">1M HIGH</label>
        <div>{monthHigh}</div>
      </div>
      <div>
        <label for="">1M LOW</label>
        <div>{monthLow}</div>
      </div>
    </div>
  </div>
</div>

<style>
  .info {
    padding-left: 2rem;
    padding-right: 2rem;
    margin-top: 2rem;
    margin-bottom: 2rem;
  }
  .info__upper {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .info__lower {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .info__lower-right {
    display: flex;
    align-items: center;
    align-items: center;
    text-align: right;
  }

  .info__lower-right > div {
    margin-left: 1rem;
  }

  .header__left-heading {
    font-size: 2rem;
  }

  .header__left-heading-price {
    font-size: 2rem;
    margin-right: 0.5rem;
  }

  label {
    color: #696969;
  }

  .positive {
    color: seagreen;
  }

  .negative {
    color: orangered;
  }

  @media (max-width: 500px) {
    .info__upper {
      flex-direction: column;
      justify-content: center;
      white-space: nowrap;
    }

    .info__lower {
      flex-direction: column;
      justify-content: center;
    }
    .info__lower-right {
      text-align: center;
    }
    .info__lower-left {
      text-align: center;
      margin-bottom: 1rem;
    }
  }
</style>
