<script lang="ts">
  import "../app.css";
  import favicon from "$lib/assets/favicon.png";

  let { children } = $props();
</script>

<svelte:head>
  <link rel="icon" href={favicon} />
  <style>
    @import url("https://fonts.googleapis.com/css2?family=Saira+Stencil+One&family=Saira:ital,wght@0,100..900;1,100..900&display=swap");
	
	body {
      font-family: "Saira", sans-serif;
      font-optical-sizing: auto;
      font-style: normal;
      font-variation-settings: "wdth" 100;
	  background: url("bg.svg");
	  background-position: right;
    }

    .saira-stencil {
      font-family: "Saira Stencil One", sans-serif;
      font-weight: 400;
      font-style: normal;
    }

	@font-face {
		font-family: "DS-Digital";
		src: url("DS-DIGIB.ttf");
	}

    .clock-font {
      font-family: "DS-Digital", monospace;
    }
  </style>
</svelte:head>

{@render children?.()}
