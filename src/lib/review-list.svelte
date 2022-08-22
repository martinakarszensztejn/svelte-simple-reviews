<script lang="ts">
  import { each } from "svelte/internal";
  import type * as types from "../types";
  export let reviewsList: types.Review[];
</script>

<div>
  {#each reviewsList as { description, rating } (rating)}
    <div class="review-container">
      <span class="rating">Rating: {rating}</span>
      <br>
      <span class="review">Description: {description}</span>
    </div>
  {/each}
</div>

<style>
  .review-container {
    background-color: white;
    margin-bottom: 10px;
    padding: 20px;
  }
  .review {
    font-size: 16pt;
    color: black;
  }
  .rating {
      font-size: 18pt;
      color: green;
      font-weight: bold;
      margin-right: 10px;
  }
</style>
