<script>
import { Link } from 'svelte-routing';

  export let product;
 
</script>

<Link  to={`/product/${product.id}`}>
<div
  class="flex flex-col max-h-[130rem] cursor-pointer max-w-80 hover:-translate-y-1 hover:scale-105 duration-300 bg-white border border-slate-200 shadow shadow-slate-950/5 rounded-2xl overflow-hidden"
>

  <!-- Product Image -->
  <img class="object-contain h-48 mt-3" src={product.image} alt="Product Image" />
  
  <!-- Product Details -->
  <div class="flex-1 flex flex-col p-6">
    <!-- Product Title -->
    <header class="mb-2 flex-2">
      <h2 class="text-lg line-clamp-2 font-extrabold leading-snug text-slate-600">
        {product.title}
      </h2>
    </header>

    <!-- Product Rating and Reviews -->
    <div class="flex gap-2">
      {#if product.rating}
        <svg class="inline-block h-5 w-5 text-yellow-400" fill="currentColor" viewBox="0 0 20 20">
          <path d="M10 15l-3.092 1.623 0.591-3.443-2.52-2.453 3.461-0.502 1.56-3.15 1.56 3.15 3.461 0.502-2.52 2.453 0.591 3.443L10 15z" />
        </svg>
      {/if}
      <div>{product.rating ? product.rating.rate : 'No Rating'}</div>
      <div>Reviews: <span>{product.rating ? product.rating.count : 'N/A'}</span></div>
    </div>

    <!-- Product Price -->
    <div class="text-base line-clamp-2 font-extrabold text-slate-500 leading-snug mt-2">
      <h2>${product.price}</h2>
    </div>

    <!-- Product Category -->
    <div class="flex mt-1 space-x-2">
      <div class="justify-start flex-1">
        <span class="inline-flex items-center rounded-md bg-blue-50 px-2 py-1 text-xs font-medium text-blue-700 ring-1 ring-inset ring-blue-700/10">
          <span>{product.category}</span>
        </span>
      </div>
      <div class="justify-end space-x-2">
        <!-- Add to Favourites Button -->
        <button on:click|stopPropagation={() => console.log('Add to Favourites')}>
          <svg class="me-1.5 h-5 w-5 hover:fill-red-500" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" transform="scale(1.6)">
            <path stroke="currentColor" strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M12.01 6.001C6.5 1 1 8 5.782 13.001L12.011 20l6.23-7C23 8 17.5 1 12.01 6.002Z" />
          </svg>
        </button>
        <!-- Add to Cart Button -->
        <button class="bg-gray-200 hover:bg-gray-300 px-2 py-1 rounded-lg">
         <p>Add to cart</p>
        </button>
      </div>
    </div>
  </div>
</div>
</Link>
