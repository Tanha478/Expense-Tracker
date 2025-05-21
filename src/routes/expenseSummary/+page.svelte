<script>
  import { onMount } from "svelte";
  
  let expenses = [];

  let dailyTotals = $state({});

  onMount(() => {
        let expenseStr = localStorage.getItem("expenses");
    expenses = expenseStr ? JSON.parse(expenseStr) : [];
    dailyTotals = getDailyTotals(expenses); // ✅ Ye automatically total calculate karega
  });

/**
   * @param {{ amount: number, category: string, note: string, date: string }[]} expenses
   */
  function getDailyTotals(expenses) {
    /** @type {{ [date: string]: number }} */
    const dailyTotals = {};

    expenses.forEach(expense => {
      if (!dailyTotals[expense.date]) {
        dailyTotals[expense.date] = 0;
      }
      dailyTotals[expense.date] += expense.amount;
    });

    return dailyTotals;
  }
</script>

{#if Object.keys(dailyTotals).length > 0}
<h1 class="stylistText text-4xl text-center relative font-bold text-[#3c5535] top-2 mt-4 mb-6">Daily Expenses</h1>
  <div class="h-full w-full flex flex-wrap gap-x-2 ">
    {#each Object.entries(dailyTotals) as [date, total]}
      <div class="bg-slate-100 h-[150px] w-[280px] border-4 border-[#dbe7d2] border-solid rounded-lg shadow-lg p-4 m-2 text-center space-y-1.5 hover:bg-[#bfe0a5]">
        <h1 class="font-poppins text-mc text-[#3c5535]">Daily Expenses</h1>
        <h1 class="text-[#3c5535]"><strong>{date}</strong>:</h1>
        <h1 class="text-[#3c5535]"> ₹{total} </h1>
  </div>
    {/each}
</div>
{:else}
  <p class="text-center text-[#4b6b42]">No expenses recorded yet.</p>
{/if}

<style>
    .stylistText {
        font-family: 'Dancing Script', cursive;
    }
</style>