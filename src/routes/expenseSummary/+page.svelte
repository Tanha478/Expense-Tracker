<script>
  import { onMount } from "svelte";
  
  let expenses = [];

  let dailyTotals = $state({});
  let weeklyTotals = $state({});
  let monthlyTotals = $state({});


  onMount(() => {
        let expenseStr = localStorage.getItem("expenses");
        expenses = expenseStr ? JSON.parse(expenseStr) : []; 

        dailyTotals = getDailyTotals(expenses); 
        weeklyTotals = getWeeklyTotals(expenses);
        monthlyTotals = getMonthlyTotals(expenses);

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

  /**
   * @param {{ amount: number, category: string, note: string, date: string }[]} expenses
   */
  function getWeeklyTotals(expenses) {
    /** @type {{ [weekStart: string]: number }} */
    const totals = {};
    expenses.forEach(expense => {
      let weekStart = getWeekStart(expense.date);
      if (!totals[weekStart]) totals[weekStart] = 0;
      totals[weekStart] += expense.amount;
    });
    return totals;
  }
   
   /**
   * @param {{ amount: number, category: string, note: string, date: string }[]} expenses
   */
   function getMonthlyTotals(expenses) {
    /** @type {{ [month: string]: number }} */
    const totals = {};
    expenses.forEach(expense => {
      let month = expense.date.slice(0, 7);
      if (!totals[month]) totals[month] = 0;
      totals[month] += expense.amount;
    });
    return totals;
  }
  
  /**
   * @param {string} dateStr
   */
  function getWeekStart(dateStr) {
    const date = new Date(dateStr);
    date.setDate(date.getDate() - date.getDay());
    return date.toISOString().split("T")[0];
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

{#if Object.keys(weeklyTotals).length > 0}
<h1 class="stylistText text-4xl text-center relative font-bold text-[#3c5535] top-2 mt-4 mb-6">Weekly Expenses</h1>
<div class="h-full w-full flex flex-wrap gap-x-2 ">
  {#each Object.entries(weeklyTotals) as [week, total]}
  <div class="bg-slate-100 h-[150px] w-[280px] border-4 border-[#dbe7d2] border-solid rounded-lg shadow-lg p-4 m-2 text-center space-y-1.5 hover:bg-[#bfe0a5]">
    <h1 class="font-poppins text-mc text-[#3c5535]">Weekly Expenses</h1>
    <h1 class="text-[#3c5535]"><strong>{week}  to  {new Date(new Date(week).setDate(new Date(week).getDate() + 6)).toISOString().split('T')[0]}
</strong></h1>
     <h1 class="text-[#3c5535]"> ₹{total}</h1>
  </div>
  {/each}
</div>
{:else}
  <p class="text-center text-[#4b6b42]">No expenses recorded yet.</p>
{/if}

{#if Object.keys(monthlyTotals).length > 0}
<h1 class="stylistText text-4xl text-center relative font-bold text-[#3c5535] top-2 mt-4 mb-6">Monthly Expenses</h1>
<div class="h-full w-full flex flex-wrap gap-x-2 ">
  {#each Object.entries(monthlyTotals) as [month, total]}
  <div class="bg-slate-100 h-[150px] w-[280px] border-4 border-[#dbe7d2] border-solid rounded-lg shadow-lg p-4 m-2 text-center space-y-1.5 hover:bg-[#bfe0a5]">
    <h1 class="font-poppins text-mc text-[#3c5535]">Monthly Expenses</h1>
    <h1 class="text-[#3c5535]"><strong>{month}</strong>:</h1>
      <h1 class="text-[#3c5535]"> ₹{total}</h1>
  </div>
  {/each}
</div>
{:else}
  <p class="text-center text-[#4b6b42]">No expenses recorded yet.</p>
{/if}



<style>
    .stylistText {
        font-family: monospace;
    }
</style>