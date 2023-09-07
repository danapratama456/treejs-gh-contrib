<script lang="ts">
  import { onMount } from "svelte";
  import { T } from "@threlte/core";
  import { Center, Grid, OrbitControls } from "@threlte/extras";
  import type { Contributions } from "$lib/types";

  export let nama = "danapratama456";
  export let tahun = 2020;

  let contributions: Contributions[] = [];

  function getColor(level: number) {
    switch (level) {
      case 0:
        return "#0e0e0e";
      case 1:
        return "#00442a";
      case 2:
        return "#006d35";
      case 3:
        return "#00a648";
      case 4:
        return "#00d35c";
    }
  }

  function normalize(count: number, base = 4, offset = 2) {
    switch (true) {
      case count === 0:
        return base;
      case count > 40:
        return count;
      default:
        return count * (base + offset);
    }
  }
  onMount(async () => {
    const response = await fetch(
      `https://scraping-gh-contribution.vercel.app/${nama}/${tahun}`
    );
    contributions = await response.json();
  });
</script>

<T.PerspectiveCamera makeDefault position={[10, 500, 100]} fov={60}>
  <OrbitControls enableDamping autoRotate />
</T.PerspectiveCamera>

<T.AmbientLight color="#fff" intensity={0.4} />
<T.DirectionalLight position={[0, 200, 200]} intensity={2} color="#fff" />
<T.DirectionalLight position={[0, 200, -200]} color="#fff" intensity={2} />

<Center autoCenter position.y={100}>
  {#each contributions as row, i}
    {#each row as day, j}
      {#if day}
        {@const color = getColor(day.level)}
        {@const y = normalize(day.count)}
        <T.Group position={[0, 0, 12 * i]}>
          <T.Mesh position={[12 * j, y / 2, 0]}>
            <T.BoxGeometry args={[10, y, 10]} />
            <T.MeshStandardMaterial {color} />
          </T.Mesh>
        </T.Group>
      {/if}
    {/each}
  {/each}
</Center>
