<script>
    import { redirect } from "@sveltejs/kit";
</script>


<div class="h-full w-full ">
    <div class="backImage h-[30vh] w-full flex justify-center item-center bg-[url('/anot.jpg')] bg-cover bg-center">
        <h1 class="stylistText text-6xl relative font-bold text-[#3c5535] top-20">Expense Tracker</h1>

         <!-- <button class="mt-4 px-6 py-3 bg-[white] text-[#3c5535] font-bold rounded-lg shadow-md hover:bg-[#3c5535] hover:text-[white] transition duration-300">
            Get Started
        </button> -->

    </div>
    <h1 class=" travisHead text-center font-serif font-bold mt-6 hover:text-[#3c5535] cursor-pointer">Track your food Expenses</h1>
    <div class="h-[50vh] w-full flex items-center justify-center gap-15">

        <a href="/expenseForm" aria-label="Go to Add Daily Expense">
    <div class="h-60 w-60  bg-slate-100 text-center space-y-4 p-3 border border-transparent rounded-sm  hover:bg-slate-200">
        <i class="fa-solid fa-cart-plus"></i>
        <h2 class="font-bold">Add Daily Expense</h2>
        <p>Write down all the expenses according to their category.</p>
        <i class="fa-solid fa-arrow-right"></i>
    </div>
        </a>

        <a href="/expenseList" aria-label="Go to Expense List">
    <div class="h-60 w-60  bg-slate-100  text-center space-y-4 p-3 border border-transparent rounded-sm  hover:bg-slate-200">
        <i class="fa-solid fa-wallet"></i>
        <h2 class="font-bold">Expense List</h2>
        <p>List of record of daily expenses in different categories.</p>
        <i class="fa-solid fa-arrow-right"></i>
    </div>
        </a>

    <a href="/expenseSummary" aria-label="Go to Expense Summary">
    <div class="h-60 w-60  bg-slate-100  text-center space-y-4 p-3 border border-transparent rounded-sm  hover:bg-slate-200">
        <i class="fa-solid fa-money-bill-wave"></i>
        <h2 class="font-bold">Expense Summary</h2>
        <p>The total expenses for every category, as well as daily expenses.</p>
        <i class="fa-solid fa-arrow-right"></i>
    </div>
    </a>

</div>
</div>

<style>
    .backImage {
        margin-top: -70px;
    }
    .stylistText {
        font-family: monospace;
    }
    .travisHead:hover{
     color: #3c5535;
     cursor: pointer;
    }
</style>