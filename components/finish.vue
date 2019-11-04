<template>
	<div class="c-finish">
		<h2 class="c-finish__title">toujours indécise ?	découvrez nos teintes <span>mates</span> best sellers</h2>
		<div class="c-finish__related">
			<div class="c-finish__related__item">
				<div class="c-finish__related__img">					
        			<img src="https://via.placeholder.com/400x375" alt="">
				</div>
				<h3 class="c-finish__related__title">01. ALWAYS RED</h3>
				<a class="c-finish__related__link" href="">ajouter au panier</a>
			</div>
			<div class="c-finish__related__item">
				<div class="c-finish__related__img">					
        			<img src="https://via.placeholder.com/400x375" alt="">
				</div>
				<h3 class="c-finish__related__title">01. ALWAYS RED</h3>
				<a class="c-finish__related__link" href="">ajouter au panier</a>
			</div>
			<div class="c-finish__related__item">
				<div class="c-finish__related__img">					
        			<img src="https://via.placeholder.com/400x375" alt="">
				</div>
				<h3 class="c-finish__related__title">01. ALWAYS RED</h3>
				<a class="c-finish__related__link" href="">ajouter au panier</a>
			</div>
		</div>

	    <div class="b-valider">
	      <div class="b-valider__item" @click="backToProduct"><span></span>Retour</div>
	    </div>

	</div>
</template>

<script>

	export default {
		methods:{
			backToProduct(){
				this.$emit('backToProduct')
			},
		}
	}

</script>

<style lang="scss">
	@import "~/assets/scss/variables/_utils.scss";
	.c-finish{		
	    position: relative;
	    z-index: 1;
	    height: 100%;
	    &__title{
			text-transform: uppercase;
			text-align: center;
			font-size: 25px;
			line-height: 30px;
			margin-bottom: 55px;
			position: relative;
			top: 15px;
			font-family: AvalonBoldOblique;
			span{
				color: $color-primary;
			}
	    }
	    &__related{
	    	overflow: auto;
	    	white-space: nowrap;
	    	padding-left: 22px;
	    	&__item{
	    		display: inline-block;
	    		white-space: nowrap;
	    		margin-right: 20px;
	    		max-width: 66%;
	    		text-align: center;
	    	}
	    	&__img{
				border-radius: 15px;
				overflow: hidden;
				margin-bottom: 18px;
	    	}
	    	&__title{
	    		font-family: AvalonBold;
	    		font-size: 13.5px;
	    		margin-bottom: 16px;
	    	}
	    	&__link{	    		
				background: $color-black;
				text-align: center;
				color: $color-white;
				border-radius: 15px;
				text-transform: uppercase;
				font-size: 9.5px;
				padding: 10px;
				letter-spacing: 1.7px;
			    width: 78%;
				margin: auto;
				display: inline-block;
	    	}
	    }
	}
</style>