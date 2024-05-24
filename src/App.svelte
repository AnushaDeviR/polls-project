<script>
  import Footer from "./components/Footer.svelte";
  import Header from "./components/Header.svelte";
  import Tabs from "./reuseable/Tabs.svelte";
  import CreatePollsForm from "./components/CreatePollsForm.svelte";

  // Tabs
  const CURRENT_POLLS = "Current Polls";
  const ADD_NEW_POLL = "Add New Poll";

  let tabList = [CURRENT_POLLS, ADD_NEW_POLL];
  let activeTab = CURRENT_POLLS;

  let polls = [
    {
      id: 1,
      question: "Python or JavaScript",
      answerA: "Python",
      answerB: "JavaScript",
      votesA: 9,
      votesB: 15,
    },
  ];

  const handleTabChange = (e) => {
    activeTab = e.detail;
  };

  const handleAddPoll = (e) => {
    console.log(e);
    const poll = e.detail;
    polls = [poll, ...polls];
    console.log("[CMD] 🐨 | handleAddPoll | polls:", polls);
  };
</script>

<Header />

<main>
  <Tabs {tabList} {activeTab} on:handleTabChange={handleTabChange} />
  {#if activeTab === CURRENT_POLLS}
    <CreatePollsForm />
  {:else if activeTab === ADD_NEW_POLL}
    <CreatePollsForm on:add={handleAddPoll} />
  {/if}
</main>

<Footer />

<style>
  main {
    max-width: 960px;
    margin: 40px auto;
  }
</style>
