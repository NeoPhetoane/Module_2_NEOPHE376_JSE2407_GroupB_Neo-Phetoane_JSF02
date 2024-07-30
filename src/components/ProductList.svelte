<script>
  import ProductCard from './ProductCard.svelte';
  import FilterSort from './FilterSort.svelte';
  import { onMount } from 'svelte';
  
  let products = [];
  let categories = [];
  let selectedCategory = "";
  let sortOrder = "default";
  let loading = true;
  let error = null;

  async function fetchProducts() {
    try {
      loading = true;
      const response = await fetch("https://fakestoreapi.com/products");
      products = await response.json();
    } catch (err) {
      error = err;
    } finally {
      loading = false;
    }
  }

  async function fetchCategories() {
    try {
      const response = await fetch("https://fakestoreapi.com/products/categories");
      categories = await response.json();
    } catch (err) {
      error = err;
    }
  }

  function handleFilterChange(category) {
    selectedCategory = category;
    loadProducts();
  }

  function handleSortChange(order) {
    sortOrder = order;
    loadProducts();
  }

  async function loadProducts() {
    try {
      loading = true;
      const response = await fetch(https://fakestoreapi.com/products);
      let allProducts = await response.json();

      // Filter products by selected category
      if (selectedCategory) {
        allProducts = allProducts.filter(product => product.category === selectedCategory);
      }

      // Sort products by price
      if (sortOrder === 'asc') {
        allProducts.sort((a, b) => a.price - b.price);
      } else if (sortOrder === 'desc') {
        allProducts.sort((a, b) => b.price - a.price);
      }

      products = allProducts;
    } catch (err) {
      error = err;
    } finally {
      loading = false;
    }
  }

  onMount(() => {
    fetchCategories();
    loadProducts();
  });
  
</script>

<FilterSort {categories} onFilterChange={handleFilterChange} onSortChange={handleSortChange} />

<!-- Loading State -->
{#if loading && !error}
  <div class="grid justify-center">
    <div class="lg:max-h-[130rem] max-w-xl mx-auto grid gap-4 grid-cols-1 lg:grid-cols-4 md:grid-cols-2 items-center lg:max-w-none my-4">
      {#each Array(20) as _, index}
        <div class="bg-white max-w-sm p-4 border border-gray-200 rounded shadow animate-pulse md:p-6 dark:border-gray-700" key={index}>
          <div class="flex items-center justify-center h-48 mb-4 bg-gray-300 rounded dark:bg-gray-700">
            <svg class="w-10 h-10 text-gray-200 dark:text-gray-600" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor" viewBox="0 0 16 20">
              <path d="M14.066 0H7v5a2 2 0 0 1-2 2H0v11a1.97 1.97 0 0 0 1.934 2h12.132A1.97 1.97 0 0 0 16 18V2a1.97 1.97 0 0 0-1.934-2ZM10.5 6a1.5 1.5 0 1 1 0 2.999A1.5 1.5 0 0 1 10.5 6Zm2.221 10.515a1 1 0 0 1-.858.485h-8a1 1 0 0 1-.9-1.43L5.6 10.039a.978.978 0 0 1 .936-.57 1 1 0 0 1 .9.632l1.181 2.981.541-1a.945.945 0 0 1 .883-.522 1 1 0 0 1 .879.529l1.832 3.438a1 1 0 0 1-.031.988Z"/>
              <path d="M5 5V.13a2.96 2.96 0 0 0-1.293.749L.879 3.707A2.98 2.98 0 0 0 .13 5H5Z"/>
            </svg>
          </div>
          <div class="h-2 bg-gray-200 rounded-full dark:bg-gray-700 mb-2.5"></div>
          <div class="h-2.5 bg-gray-200 rounded-full dark:bg-gray-700 w-48 mb-4"></div>
          <div class="h-2.5 bg-gray-200 rounded-full dark:bg-gray-700 w-10 mb-4"></div>
          <span class="sr-only">Loading...</span>
        </div>
      {/each}
    </div>
  </div>
{/if}

<!-- Error State -->
{#if error}
  <div class="grid justify-center">
    <div class="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative" role="alert">
      <strong class="font-bold">Error:</strong>
      <span class="block sm:inline">{error.message}</span>
    </div>
  </div>
{/if}

<!-- Product Cards -->
{#if !loading && !error}
  <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
    {#each products as product}
      <ProductCard {product} onClick={id => console.log(id)} />
    {/each}
  </div>
{/if}