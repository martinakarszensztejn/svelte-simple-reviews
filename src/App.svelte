<script lang="ts">
  import SetReviewsModule from "./lib/submit-review.svelte";
  import ReviewAnalyticsModule from "./lib/review-analytics.svelte";
  import ReadReviewsModule from "./lib/review-list.svelte";
  import type * as types from "./types";
  let reviewsList: types.Review[] = [];
</script>

<main>
  <SetReviewsModule bind:reviewsList />
  <ReviewAnalyticsModule {reviewsList} />
  <ReadReviewsModule {reviewsList} />
  <p>This is the end, sadly</p>
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  }

  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }
</style>
