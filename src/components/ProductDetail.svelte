<script>
  import { onMount } from 'svelte';
  import { params} from 'svelte-spa-router';
  import {Link } from 'svelte-routing';

  let product = {};
  let { id } = params();

  onMount(async () => {
    const response = await fetch(`https://fakestoreapi.com/products/${productId}`);
    product = await response.json();
  });
</script>
<main>
{#if $product}
<div class="p-4">
  <h1 class="text-3xl font-bold">{product.title}</h1>
  <img src={product.image} alt={product.title} class="w-full" />
  <p>{product.description}</p>
  <p>${product.price}</p>
  <p>{product.category}</p>
  <p>Rating: {product.rating ? product.rating.rate : 'N/A'}</p>
  <p>Reviews: {product.rating ? product.rating.count : 'N/A'}</p>
</div>
{:else}
<p>Loading...</p>
{/if}
<Link to="/"> Back</Link>
</main>