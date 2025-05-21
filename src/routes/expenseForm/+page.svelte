<script>
  let amount = "";
  let category = "Groceries";
  let note = "";
  let date = new Date().toISOString().split("T")[0];

  function addExpense() {
    const expense = { amount, category, note, date };
    const expensesStr = localStorage.getItem("expenses");
    let expenses = expensesStr ? JSON.parse(expensesStr) : [];
    expenses.push(expense);
    localStorage.setItem("expenses", JSON.stringify(expenses));
    
    // Clear form after adding
    amount = "";
    category = "Groceries";
    note = "";
    date = new Date().toISOString().split("T")[0];
  }
</script>

<div class="max-w-lg mx-auto bg-[#dbe7d2] p-6 rounded-lg shadow-lg mt-7">
    <h2 class="text-2xl font-bold text-[#3c5535] mb-4 text-center">Add Expense</h2>

<form on:submit|preventDefault={addExpense} class="space-y-4">
    <div>
        <label for="amount" class="block text-[#3c5535] font-semibold">Amount (₹)</label>
  <input id="amount" type="number" bind:value={amount} placeholder="Amount (₹)" class="w-full p-2 border border-[#3c5535] rounded-lg focus:ring-2 focus:ring-[#3c5535]"
 required />
    </div>

  <div>
    <label for="category" class="block text-[#3c5535] font-semibold">Category</label>
  <select id="category" bind:value={category} class="w-full p-2 border border-[#3c5535] rounded-lg focus:ring-2 focus:ring-[#3c5535]">
    <option>Groceries</option>
    <option>Restaurant</option>
    <option>Takeout</option>
    <option>Other</option>
  </select>
  </div>

  <div>
    <label for="note" class="block text-[#3c5535] font-semibold">Note</label>
  <input id="note" type="text" bind:value={note} placeholder="Note" class="w-full p-2 border border-[#3c5535] rounded-lg focus:ring-2 focus:ring-[#3c5535]" />
  </div>
    
  <div>
     <label for="date" class="block text-[#3c5535] font-semibold">Date</label>
  <input id="date" type="date" bind:value={date} class="w-full p-2 border border-[#3c5535] rounded-lg focus:ring-2 focus:ring-[#3c5535]" />
  </div>

  <button type="submit" class="w-full bg-[#3c5535] text-white p-2 rounded-lg hover:bg-[#2a3d24] transition">Add Expense</button>
</form>
</div>