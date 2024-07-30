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
  <p>Loading...</p>
{:else if error}
  <p>Error: {error}</p>
{:else}
  <div class="product-detail">
    <button on:click={goBack}>Back to Products</button>
    <h1>{product.title}</h1>
    <img src={product.image} alt={product.title} />
    <p>{product.description}</p>
    <p>Price: ${product.price}</p>
    <p>Category: {product.category}</p>
    <p>Rating: {product.rating.rate} ({product.rating.count} reviews)</p>
  </div>
{/if}