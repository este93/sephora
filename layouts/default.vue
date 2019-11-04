<template>
  <div id="wrapper">
    <Header />
    <nuxt/>
  </div>
</template>

<script>
import Header from '~/components/header'

export default {
  components: {
    Header
  },
}

</script>


<style lang="scss">
	#wrapper{
		height: 100vH;
	}
</style>

