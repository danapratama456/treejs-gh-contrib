<script lang="ts">
  import { Canvas } from "@threlte/core";
  import Scene from "$lib/components/Scene.svelte";

  // let nama: string;
  // let tahun: number;
</script>

<svelte:head>
  <title>Github Contribution three js</title>
</svelte:head>

<div class="scene">
  <!-- <input type="text" bind:value={nama} />
  <input type="text" bind:value={tahun} /> -->
  <Canvas>
    <Scene {nama} {tahun} />
  </Canvas>
</div>

<style>
  .scene {
    position: absolute;
    inset: 0;
    background-color: hsl(214, 56%, 8%);
  }
</style>
