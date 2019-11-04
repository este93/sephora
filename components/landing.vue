<template>
	<div class="c-landing">
		
        <div class="c-btn--wraper" @click="start" href=""><span class="c-btn c-btn--start">Commencer</span></div>

	</div>
</template>

<script>

	export default {
		methods:{
			start(){
				this.$emit('start')
			}
		}
	}

</script>

<style lang="scss">
	@import "~/assets/scss/variables/_utils.scss";
	.c-landing{
		background: url(../assets/images/hp-back2.jpg);
		background-size: cover;
		background-position: center center;
		height: 100%;
		.c-btn--wraper{
			position: absolute;
			bottom: 26px;
			left: 0;
			right: 0;
			z-index: 1;
		}
	}
</style>