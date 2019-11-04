<template>
	<div class="c-product">

		<div class="c-product__item">
			<h2 class="c-product__item__title">{{ itemSelected.category }} <span>{{ itemSelected.parent }}</span></h2>
			<h2 class="c-product__item__subtitle">{{ itemSelected.title }}</h2>
			<div class="c-product__item__img">				
        		<img src="https://via.placeholder.com/455x455" alt="">
			</div>
			<div class="c-product__item__color">
				<span :style="'background:' + itemSelected.colors[color].color">{{ itemSelected.colors[color].number }}</span>
				always red
			</div>
			<div class="c-product__item__price">{{ itemSelected.price }}</div>
			<div class="c-product__item__link">ajouter au panier</div>
		</div>

	    <div class="b-valider--product b-valider">
	      <div class="b-valider__item" @click="back"><span></span>Retour</div>
	      <div class="b-valider__item" @click="finish">voir nos autres teintes best sellers</div>
	    </div>

	</div>
</template>

<script>
	export default {
		props: ['itemSelected', 'color'],
		methods:{
			finish(){
				this.$emit('finish')
			},
		    back(){
		      this.$emit('backToColors');
		    }
		}
	}
</script>

<style lang="scss">
	@import "~/assets/scss/variables/_utils.scss";
	.c-product{		
	    position: relative;
	    z-index: 1;
    	height: 100%;
    	&__item{
    		position: relative;
    		top: 20px;
    		z-index: 1;
    		text-align: center;
			border-radius: 15px;
			background-color: rgb(244, 242, 250);
			box-shadow: 0px 0px 34.4px 8.6px rgba(0, 0, 0, 0.19);
			max-width: 79%;
			margin: auto;
			text-transform: uppercase;
			padding: 16px 20px 0 20px;
			box-sizing: border-box;
			&__title{
				font-family: AvalonBoldOblique;
				font-size: 15px;
				span{
					color: $color-primary;
				}
			}
			&__subtitle{
				font-family: AvalonBoldOblique;
				font-size: 12px;
				color: $color-primary;
				margin-bottom: 20px;
			}
			&__img{
				margin-bottom: 20px;
			}
			&__color{
				font-family: AvalonBold;
				font-size: 17px;
				margin-bottom: 6px;
				span{					
			        text-align: center;
			        width: 31px;
			        line-height: 31px;
			        border-radius: 100%;
			        background: black;
			        color: $color-white;
			        font-family: AvalonBold;
			        font-size: 10.5px;
			        display: inline-block;
			        vertical-align: middle;
			        margin-right: 3px;
				}
			}
			&__price{
				font-family: AvalonBold;
				font-size: 18px;
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
			    width: 71%;
				margin: auto;
				position: relative;
				top: 15px;
			}
    	}
	}
	.b-valider--product{
    	color: $color-black;
    	.b-valider__item{
    		&:nth-child(2){
    			border: 2px solid $color-black;
    			border-radius: 20px;
    			text-transform: uppercase;
    			font-size: 10px;
    			line-height: 28px;
    			padding: 0 6px;
    			letter-spacing: -0.1px;
    			height: 27px;
    		}
    	}
		span{
        	background: url(../assets/images/arrow-black.png) no-repeat center center; 
        	background-size: 8.5px 13px;
    		border-color: $color-black;
		}
	}
</style>