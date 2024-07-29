<script>
  import { onMount } from 'svelte';
  let products = [];
  let isLoading = true;
  let error = null;
  
  const fetchProduct = 'https://fakestoreapi.com/products';

  onMount(async () => {
    try {
      const response = await fetch(fetchProduct);
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      products = await response.json();
    } catch (err) {
      error = err.message;
    } finally {
      isLoading = false;
    }
  });
</script>



<div>
  {#if isLoading}
    <div class="loading">Loading products...</div>
  {:else if error}
    <div class="error">Error: {error}</div>
  {:else}
    <div class="product-grid">
      {#each products as product}
        <div class="product-card">
          <img src={product.image} alt={product.title} class="product-image" />
          <div class="product-info">
            <div class="product-title">{product.title}</div>
            <div class="product-price">${product.price}</div>
            <div class="product-category">{product.category}</div>
          </div>
        </div>
      {/each}
    </div>
  {/if}
</div>