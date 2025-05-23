<script>
    import { onMount } from "svelte";
    import {writable} from "svelte/store";

    /** @type {{ amount: number, category: string, note: string, date: string }[]} */
    let expenses = $state([]);
    onMount(() => {
        let expenseStr = localStorage.getItem("expenses");
        expenses = expenseStr ? JSON.parse(expenseStr) : [];
    });


    /** @param {number} index */
    function deleteExpense(index){
        expenses.splice(index, 1);
        localStorage.setItem("expenses", JSON.stringify(expenses));
    }

</script>

<h1 class="stylistText text-4xl text-center relative font-bold text-[#3c5535] top-2 mb-6">Expense List</h1>
<div class="h-full w-full flex flex-wrap gap-x-2 ">
{#if expenses.length > 0}
    {#each expenses.slice().reverse() as expense , index}
    <div class="bg-slate-100 h-[200px] w-[280px] border-4 border-[#dbe7d2] border-solid rounded-lg shadow-lg p-4 m-2 text-center space-y-1.5 hover:bg-[#bfe0a5]">
        <h1 class="font-poppins text-mc text-[#3c5535]">Amount = <strong>₹{expense.amount}</strong> ({expense.category})</h1>
    
        <p  class="text-sm text-gray-700">Note: <small>{expense.note}</small></p>
        
        <p class="text-sm text-gray-700">Date: {expense.date}</p>
        
        <button class=" buttoonn mt-3 px-4 py-2 border-2 border-[#4b6b42] bg-[#4b6b42] border-solid rounded-lg shadow text-white" onclick={() => {
            deleteExpense(expenses.length - 1 - index);
        }}>Delete</button>
    </div>
    {/each}
{:else}
<p class="text-center text-[#4b6b42]">No expenses added yet.</p>
{/if}
</div>

<style>
     .stylistText {
        font-family: monospace;
    }
    .buttoonn:hover {
        background-color: aliceblue;
        border-color:#4b6b42 ;
        color: #4b6b42;
    }
</style>