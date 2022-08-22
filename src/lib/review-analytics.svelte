<script lang="ts">
  import type * as types from "../types";
  export let reviewsList: types.Review[];
</script>

<div class="container">
  <span class="elem">Reviews: {reviewsList.length}</span>
  <span class="elem"
    >Ratings Average: {reviewsList.length > 0
      ? (
          reviewsList.reduce((tot, curr) => tot + curr.rating, 0) /
          reviewsList.length
        ).toFixed(2)
      : "No reviews"}</span
  >
</div>

<style>
  .elem {
    margin-top: 15px;
    color: white;
    font-size: 20pt;
  }
  .container {
    display: flex;
    flex-flow: row wrap;
    justify-content: space-around;
  }
</style>
