<script lang="ts">
  let { name }: { name: string } = $props();

  const thumbnailModules = import.meta.glob<string>(
    "$lib/assets/demo-thumbnails/*.svg",
    {
      eager: true,
      import: "default",
    },
  );

  const thumbnails = Object.fromEntries(
    Object.entries(thumbnailModules).map(([path, src]) => [
      path.match(/\/([^/]+)\.svg$/)?.[1] ?? path,
      src,
    ]),
  );
</script>

<img
  class="thumb-img"
  src={thumbnails[name] ?? thumbnails.fallback}
  alt=""
  draggable="false"
  loading="lazy"
  decoding="async"
/>

<style>
  .thumb-img {
    display: block;
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
</style>
