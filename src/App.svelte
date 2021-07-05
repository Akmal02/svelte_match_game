<script lang="ts">
  import PlayScreen from "./components/PlayScreen.svelte";
</script>

<main>
  <PlayScreen />
</main>

<style>
  main {
    background: #00f260; /* fallback for old browsers */
    background: -webkit-linear-gradient(
      135deg,
      #0575e6,
      #00f260
    ); /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(
      135deg,
      #0575e6,
      #00f260
    ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
</style>
