<script>
  import Header from "./components/Header.svelte";
  import Footer from "./components/Footer.svelte";
  import Tabs from "./shared/Tabs.svelte";
  import PollForm from "./components/PollForm.svelte";
  import PollList from "./components/PollList.svelte";

  let items = ["Current Polls", "Add New Poll"];
  let activeItem = "Current Polls";

  const switchTab = (e) => {
    activeItem = e.detail;
  };

  const handleSubmit = () => {
    activeItem = "Current Polls";
  };
</script>

<Header />

<main>
  <Tabs {activeItem} {items} on:switchTab={switchTab} />
  {#if activeItem === "Current Polls"}
    <PollList />
  {:else if activeItem === "Add New Poll"}
    <PollForm on:handleSubmit={handleSubmit} />
  {/if}
</main>

<Footer />

<style>
  main {
    max-width: 960px;
    margin: 3rem 0;
  }
</style>
