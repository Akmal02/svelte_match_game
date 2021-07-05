<script lang="ts">
  import { onMount } from "svelte";
  import { matchCardDataList } from "../models/matchCardData";

  import { range, shuffle } from "../utils";

  import MatchCard from "./MatchCard.svelte";

  let cardGrid: number[] = generateRandomCardGrid(36);

  let firstCard: number = null;
  let secondCard: number = null;

  let gameStarted = false;

  onMount(() => {
    setTimeout(() => {
      gameStarted = true;
    }, 1000);
  });

  $: if (firstCard != null && secondCard != null) {
    setTimeout(() => {
      if (
        cardGrid[firstCard] != null &&
        cardGrid[firstCard] == cardGrid[secondCard]
      ) {
        cardGrid[firstCard] = null;
        cardGrid[secondCard] = null;
      }
      firstCard = null;
      secondCard = null;
    }, 600);
  }

  function generateRandomCardGrid(size: number) {
    let grid = Array(size);
    for (let i = 0; i < size; i++) {
      grid[i] = Math.floor(i / 2);
    }

    return shuffle(grid);
  }

  function onCardClicked(card) {
    return () => {
      if (!gameStarted) return;

      if (firstCard == null) {
        firstCard = card;
      } else if (secondCard == null) {
        secondCard = card;
      }
    };
  }
</script>

<div class="grid">
  {#each range(0, cardGrid.length - 1) as i}
    {#if cardGrid[i] != null}
      <MatchCard
        data={matchCardDataList[cardGrid[i]]}
        flipped={i == firstCard || i == secondCard || !gameStarted}
        on:click={onCardClicked(i)}
      />
    {:else}
      <div />
    {/if}
  {/each}
</div>

<style>
  .grid {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    width: 100%;
    gap: 16px;
    padding: 32px;
    box-sizing: border-box;
  }

  @media screen and (min-width: 800px) {
    .grid {
      width: 800px;
      margin: 0 auto;
    }
  }
</style>
