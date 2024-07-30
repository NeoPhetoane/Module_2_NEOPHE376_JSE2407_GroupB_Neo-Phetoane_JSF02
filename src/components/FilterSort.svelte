<script>

</script>

<div class="flex flex-col space-y-4 p-4 bg-white border border-gray-200 rounded-lg shadow-md">
  <!-- Category Filter -->
  <div>
    <label for="category" class="block text-sm font-medium text-gray-700">Filter by Category:</label>
    <select
      id="category"
      class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm"
      on:change={handleCategoryChange}
    >
      <option value="">All Categories</option>
      {#each categories as category}
        <option value={category}>{category}</option>
      {/each}
    </select>
  </div>

  <!-- Sort Order -->
  <div>
    <label for="sort" class="block text-sm font-medium text-gray-700">Sort by Price:</label>
    <select
      id="sort"
      class="mt-1 block w-full p-2 border border-gray-300 rounded-md shadow-sm"
      on:change={handleSortChange}
    >
      <option value="default">Default</option>
      <option value="asc">Lowest to Highest</option>
      <option value="desc">Highest to Lowest</option>
    </select>
  </div>
</div>

<style>
</style>