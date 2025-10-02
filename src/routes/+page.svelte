<script lang="ts">
  import { onMount } from "svelte";
  import favicon from "$lib/assets/favicon.png";

  interface TimeCalc extends Object {
    days: number;
    hours: number;
    minutes: number;
    seconds: number;
    distance: number;
  }

  const DEFAULT_TIMECALC = {
    days: 0,
    hours: 0,
    minutes: 0,
    seconds: 0,
    distance: 0,
  };

  const shippingEnd = new Date("2025-10-02T03:59:59.000Z");
  const votingEnd = new Date("2025-10-07T03:59:59.000Z");
  const shopEnd = new Date("2025-10-11T03:59:59.000Z");

  let shippingTimeCalc: TimeCalc = $state(DEFAULT_TIMECALC);
  let votingTimeCalc: TimeCalc = $state(DEFAULT_TIMECALC);
  let shopTimeCalc: TimeCalc = $state(DEFAULT_TIMECALC);

  const countdownInterval = setInterval(function () {
    let now = new Date().getTime();

    shippingTimeCalc = getTime(shippingEnd.getTime() - now);
    votingTimeCalc = getTime(votingEnd.getTime() - now);
    shopTimeCalc = getTime(shopEnd.getTime() - now);

    if (shopEnd.getTime() - now < 0) {
      clearInterval(countdownInterval);
    }
  }, 1000);

  const getTime = (distance: number) => {
    const days = Math.floor(distance / (1000 * 60 * 60 * 24));
    const hours = Math.floor(
      (distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)
    );
    const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
    const seconds = Math.floor((distance % (1000 * 60)) / 1000);

    return { days, hours, minutes, seconds, distance } as TimeCalc;
  };

  onMount(() => {
    let now = new Date().getTime();

    shippingTimeCalc = getTime(shippingEnd.getTime() - now);
    votingTimeCalc = getTime(votingEnd.getTime() - now);
    shopTimeCalc = getTime(shopEnd.getTime() - now);
  });
</script>

<h1 class="text-6xl saira-stencil text-center mt-10">
  When does Summer of Making <span class="text-red-800">END</span>?
</h1>
<div class="flex items-center flex-col md:h-[82dvh] gap-10 p-12">
  <img src={favicon} class="h-[15rem] w-auto" alt="AAAAAAAApheus by @ren">
  <div class="w-[70vw] 2xl:ms-[28vw]">
    <h2 class="text-4xl">
      Shipping ends in <span class="text-2xl"
        >(at {shippingEnd.toLocaleString()} in your timezone)</span
      >
    </h2>
    <h2 class="text-5xl font-bold text-red-800">
      {#if shippingTimeCalc.distance < 0}
        SHIPPING HAS ENDED!!!
      {:else}
        {shippingTimeCalc.days} days {shippingTimeCalc.hours} hours {shippingTimeCalc.minutes}
        minutes {shippingTimeCalc.seconds} seconds
      {/if}
    </h2>
  </div>
  <div class="w-[70vw] 2xl:ms-[28vw]">
    <h2 class="text-4xl">
      Voting ends in <span class="text-2xl"
        >(at {votingEnd.toLocaleString()} in your timezone)</span
      >
    </h2>
    <h2 class="text-5xl font-bold text-red-800">
      {#if votingTimeCalc.distance < 0}
        VOTING HAS ENDED!!!
      {:else}
        {votingTimeCalc.days} days {votingTimeCalc.hours} hours {votingTimeCalc.minutes}
        minutes {votingTimeCalc.seconds} seconds
      {/if}
    </h2>
  </div>
  <div class="w-[70vw] 2xl:ms-[28vw]">
    <h2 class="text-4xl">
      Shop closes in <span class="text-2xl"
        >(at {shopEnd.toLocaleString()} in your timezone)</span
      >
    </h2>
    <h2 class="text-5xl font-bold text-red-800">
      {#if shopTimeCalc.distance < 0}
        SHOP IS CLOSED!!!
      {:else}
        {shopTimeCalc.days} days {shopTimeCalc.hours} hours {shopTimeCalc.minutes}
        minutes {shopTimeCalc.seconds} seconds
      {/if}
    </h2>
  </div>
</div>
<footer class="text-2xl text-center mb-5">by sage with :3</footer>
