<template>
  <div>
    <h2>News-Content [{{ $route.params.id }}]</h2>
    <ul>
      <li><a href="/">HOME</a></li>
    </ul>
  </div>
</template>
<script>
  	export default {

	  validate ({ params }) {
	    // Must be a number
	    return /^\d+$/.test(params.id)
	  }

	}
</script>
