<template>
	
	<div class="c-match">
	</div>

</template>


<script>

export default {	
  methods: {
    redirect(){
      const _self = this;
      setTimeout(function(){
        _self.$emit('matchDone')
      }, 2000)  
    }
  },
  mounted () { 
    this.redirect();
  }
}

</script>

<style lang="scss">
	.c-match{
		background: url(../assets/images/match.png) no-repeat;
		background-size: 80%;
		background-position: center center;
		height: 100%;
    position: relative;
	}
</style>