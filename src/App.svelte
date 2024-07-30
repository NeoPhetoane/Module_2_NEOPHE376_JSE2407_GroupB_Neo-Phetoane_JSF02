<!--Script section-->

<script>
import { Router, Route, Link } from 'svelte-routing';
import Header from './components/Header.svelte';
import ProductList from './components/ProductList.svelte';
import ProductDetail from './components/ProductDetail.svelte';
</script>


<!--Main code section-->
<Router>
  <Header />

  <main>
    <Route path="/" component={ProductList} />
    <Route path="/product/:id" component={ProductDetail} />
  </main>
</Router>


<!--Style section-->
<style>
 
</style>