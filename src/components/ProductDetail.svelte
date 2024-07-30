<script>
  import { onMount } from 'svelte';
  import { navigate } from 'svelte-routing';

  export let id;

  let product = null;
  let loading = true;
  let error = null;

  onMount(async () => {
    try {
      const response = await fetch(`https://fakestoreapi.com/products/${id}`);
      if (!response.ok) {
        throw new Error('Failed to fetch product details');
      }
      product = await response.json();
    } catch (err) {
      error = err.message;
    } finally {
      loading = false;
    }
  });

  function goBack() {
    navigate('/');
  }
</script>

{#if loading}
  <div class="flex items-center justify-center h-screen">
    <div class="text-lg text-gray-500">Loading...</div>
  </div>
{:else if error}
  <div class="flex items-center justify-center h-screen">
    <div class="text-lg text-red-600">Error: {error}</div>
  </div>
{:else}
  <div class="container mx-auto p-6 bg-white shadow-lg rounded-lg max-w-4xl">
    <button 
      class="mb-4 px-4 py-2 bg-blue-500 text-white font-semibold rounded-md shadow hover:bg-blue-600 transition duration-200"
      on:click={goBack}
    >
      Back to Products
    </button>
    <div class="flex flex-col md:flex-row gap-6">
      <img 
        class="w-full md:w-1/3 h-auto object-cover rounded-lg shadow-md"
        src={product.image} 
        alt={product.title} 
      />
      <div class="flex-1">
        <h1 class="text-3xl font-bold text-gray-800 mb-2">{product.title}</h1>
        <p class="text-gray-600 mb-4">{product.description}</p>
        <p class="text-xl font-semibold text-blue-600 mb-2">Price: ${product.price}</p>
        <p class="text-gray-700 mb-2">Category: {product.category}</p>
        <p class="text-gray-600">Rating: {product.rating.rate} ({product.rating.count} reviews)</p>
      </div>
    </div>
  </div>
{/if}

<style>
  .container {
    max-width: 1200px;
  }
</style>