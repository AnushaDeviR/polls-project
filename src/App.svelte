<script>
  import Footer from "./components/Footer.svelte";
  import Header from "./components/Header.svelte";
  import Tab from "./reuseable/Tab.svelte";
  import CreatePollsForm from "./components/CreatePollsForm.svelte";
  import PollList from "./components/PollList.svelte";

  const CURRENT_POLLS = "Current Polls";
  const ADD_NEW_POLL = "Add New Poll";

  let tabList = [CURRENT_POLLS, ADD_NEW_POLL];
  let activeTab = CURRENT_POLLS;

  const handleTabChange = (e) => {
    activeTab = e.detail;
  };

  const handleAddPoll = (e) => {
    activeTab = CURRENT_POLLS;
  };
</script>

<Header />

<main>
  <Tab {tabList} {activeTab} on:handleTabChange={handleTabChange} />
  {#if activeTab === CURRENT_POLLS}
    <PollList />
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
