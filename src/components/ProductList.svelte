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


<style>
  .product-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 16px;
    padding: 16px;
  }

  .product-card {
    border: 1px solid #ddd;
    border-radius: 8px;
    overflow: hidden;
    cursor: pointer;
    transition: box-shadow 0.3s ease;
  }

  .product-card:hover {
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }

  .product-image {
    width: 100%;
    height: 200px;
    object-fit: cover;
  }

  .product-info {
    padding: 16px;
  }

  .product-title {
    font-size: 18px;
    font-weight: bold;
    margin: 8px 0;
  }

  .product-price {
    color: #e60023;
    font-size: 16px;
    margin: 8px 0;
  }

  .product-category {
    font-size: 14px;
    color: #888;
  }

  .loading, .error {
    text-align: center;
    padding: 16px;
  }

  .loading {
    font-size: 18px;
    color: #666;
  }

  .error {
    color: #e60023;
  }
</style>