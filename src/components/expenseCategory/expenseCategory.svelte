<script>
  import { onMount } from "svelte";


  /** @type {{ amount: number, category: string, note: string, date: string }[]} */
  let expenses = $state([]);

  onMount(() => {
    const expensesStr = localStorage.getItem("expenses");
    expenses = expensesStr ? JSON.parse(expensesStr) : [];
  });

  
  let categoryTotals = $state({});

  onMount(() => {
    categoryTotals = getCategoryTotals(expenses);
  });


    /**
     * @param {{ amount: number, category: string, note: string, date: string }[]} expenses
     */
  function getCategoryTotals(expenses) {
    /** @type {{ [category: string]: number }} */
    const totals = {};
    expenses.forEach(expense => {
      if (!totals[expense.category]) {
        totals[expense.category] = 0;
      }
      totals[expense.category] += expense.amount;
    });
    return totals;
  }
</script>

<h1 class="stylistText text-4xl text-center relative font-bold text-[#3c5535] top-2 mb-6">Category Breakdown</h1>
<div class="w-full h-[150px] bg-[url('/anot.jpg')] bg-cover flex justify-center items-center space-x-6">
  
  {#if Object.keys(categoryTotals).length > 0}
    
      {#each Object.entries(categoryTotals) as [category, total]}
      <div class="bg-slate-100 h-[50px] w-[280px] border-4 border-white border-solid rounded-lg shadow-lg m-2 text-center space-y-1.5">
        <h1 class="text-center p-2 text-[#3c5535]"><strong>{category}</strong>: ₹{total}</h1>
      </div>

      {/each}

  {:else}
    <p class="text-center text-[#4b6b42]">No expenses recorded yet.</p>
  {/if}
</div>

<style>
    .stylistText {
        font-family: monospace;
    }
</style>