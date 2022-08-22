<script lang="ts">
  import type * as types from "../types";
  let text1 = "How would you rate your service with  us?";
  $: placeholder = "Tell us something that keeps you coming back";

  let description = "";
  export let reviewsList: types.Review[] = [];
  const getFormattedTime = (q: Date): string =>
    `${q.getFullYear()}/${
      q.getMonth() + 1 < 10 ? `0${q.getMonth()}` + 1 : q.getMonth() + 1
    }/${q.getDate() < 10 ? `0${q.getDate()}` : q.getDate()}`;

  let scores: { value: number; selected: boolean }[] = [
    { value: 1, selected: false },
    { value: 2, selected: false },
    { value: 3, selected: false },
    { value: 4, selected: false },
    { value: 5, selected: false },
    { value: 6, selected: false },
    { value: 7, selected: false },
    { value: 8, selected: false },
    { value: 9, selected: false },
    { value: 10, selected: false },
  ];
  function submitReview() {
    const currentScore = scores.find((y) => y.selected);
    if (currentScore) {
      reviewsList.push({
        description,
        timeSet: getFormattedTime(new Date()),
        rating: currentScore.value,
      });
      currentScore.selected = false;
      scores = scores;
      description = "";
    }
    reviewsList = reviewsList;
  }
  function handleLogic(val) {
    const previouslySelectedScores = scores.find((q) => q.selected);
    if (previouslySelectedScores) {
      previouslySelectedScores.selected = false;
    }
    scores.find((q) => q.value === val).selected = true;
    scores = scores;
  }
</script>

<div class="upper-component">
  <div><h1>{text1}</h1></div>
  <div class="btn-container">
    {#each scores as { value, selected }}
      <button
        {value}
        on:click={() => handleLogic(value)}
        class={selected ? "score-btn-selected" : "score-btn"}>{value}</button
      >
    {/each}
  </div>
  <div class="form-container">
    <input
      class="review-input"
      type="text"
      {placeholder}
      bind:value={description}
    />
    <button on:click={submitReview} class="review-send">Send</button>
  </div>
</div>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  }
  .btn-container {
    display: block;
    margin-bottom: 20px;
  }
  .form-container {
    display: flex;
    min-width: 15%;
    flex-direction: row;
    align-items: center;
    justify-content: space-evenly;
    margin-left: 25%;
    margin-right: 25%;
  }
  .upper-component {
    background-color: white;
    padding: 20px;
    border-radius: 10px;
  }
  .review-send {
    min-width: 5%;
    padding: 7px 10px;
    border-radius: 7px;
  }
  :hover.review-send {
    background-color: rgb(210, 154, 255);
  }
  .review-input {
    min-width: 75%;
    padding: 7px 10px;
    border-radius: 7px;
  }
  .score-btn,
  .score-btn-selected {
    background-color: rgb(235, 235, 235);
    display: inline-block;
    border-radius: 50%;
    font-weight: bold;
    margin-left: 3px;
    border: none;
    font-size: 25px;
    padding: 10px 20px;
  }
  .score-btn-selected {
    background-color: rgb(255, 238, 54);
  }

  :hover.score-btn {
    background-color: rgba(251, 205, 3, 0.215);
  }
</style>
