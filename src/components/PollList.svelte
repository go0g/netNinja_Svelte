<script>
  export let polls = [];
</script>

<style>

</style>

<div class="poll-list">
  {#each polls as poll (poll.id)}
    <h4>{poll.question}</h4>
    <p>{poll.answerA} - {poll.voteA}</p>
    <p>{poll.answerB} - {poll.voteB}</p>
    <hr />
  {/each}
</div>
