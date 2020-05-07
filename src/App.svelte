<script>
  import Header from "./components/Header.svelte";
  import Footer from "./components/Footer.svelte";
  import PollList from "./components/PollList.svelte";
  import CreatePollForm from "./components/CreatePollForm.svelte";

  import Tabs from "./shared/Tabs.svelte";

  // Tabs
  let items = ["Current Pool", "Add New Poll"];
  let activeItem = "Current Pool";

  const tabChange = e => {
    activeItem = e.detail;
  };

  let polls = [
    {
      id: 1,
      question: "Python or JavaScript",
      answerA: "Python",
      answerB: "JavaScript",
      voteA: 9,
      voteB: 12
    }
  ];

  const handleAdd = e => {
    const poll = e.detail;
    polls = [...polls, poll];
    console.log(polls);
    activeItem = "Current Pool";
  };
</script>

<style>
  main {
    max-width: 960px;
    margin: 40px auto;
  }
</style>

<Header />
<main>
  <Tabs {items} {activeItem} on:tabChange={tabChange} />
  {#if activeItem === 'Current Pool'}
    <PollList {polls} />
  {:else if activeItem === 'Add New Poll'}
    <CreatePollForm on:add={handleAdd} />
  {/if}
</main>
<Footer />
