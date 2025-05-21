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

<div>
  <h3>Category Breakdown</h3>
  {#if Object.keys(categoryTotals).length > 0}
    <ul>
      {#each Object.entries(categoryTotals) as [category, total]}
        <li><strong>{category}</strong>: ₹{total}</li>
      {/each}
    </ul>
  {:else}
    <p>No expenses recorded yet.</p>
  {/if}
</div>