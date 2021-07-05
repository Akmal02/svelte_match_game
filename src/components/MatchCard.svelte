<script lang="ts">
  import type { MatchCardData } from "../models/matchCardData";

  export let flipped = false;
  export let data: MatchCardData;
</script>

<div class="container">
  <div class="card" class:flipped on:click>
    <div class="front" />
    <div
      class="back"
      style={`background-color: ${data.backgroundColor}; color: ${data.foregroundColor}`}
    >
      <span class="material-icons">{data.icon}</span>
    </div>
  </div>
</div>

<style>
  .container {
    perspective: 1000px;
  }

  .card {
    width: 100%;
    padding-bottom: 100%;
    position: relative;

    user-select: none;

    transform-style: preserve-3d;
    transition: transform 0.5s cubic-bezier(0.25, 1, 0.5, 1);

    /* background-color: aquamarine; */
  }

  .card .front,
  .card .back {
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.12);
    border-radius: 8px;

    -webkit-backface-visibility: hidden; /* Safari */
    backface-visibility: hidden;
    padding: auto;

    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
  }

  .material-icons {
    font-size: 2.5rem;
  }

  .card .front {
    background: linear-gradient(
      135deg,
      rgba(255, 255, 255, 0.4),
      rgba(255, 255, 255, 0.6)
    );

    color: black;
  }

  .card .back {
    background-color: rgba(0, 0, 0, 1);
    color: white;
    transform: rotateX(180deg);
  }

  .card.flipped {
    transform: rotateX(180deg);
  }
</style>
