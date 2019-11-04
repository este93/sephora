<template>
  <main class="container">

	<div 
		class="c-wave--wrapper--top c-wave--wrapper" 
		:class="{
			state1 : waveState1, 
			state2 : waveState2, 
			state3 : waveState3, 
			state4 : waveState4,
			state5 : waveState5,
			state6 : waveState6,
			state7 : waveState7,
			state8 : waveState8,
			stateReset : waveStateReset
		}"
	>
		<div class="c-wave"></div>
	</div>

    <transition name="fade">
		<component 
			:is="component" 
			@start = "start"
			@likeCard = "likeCard"
			@matchDone = "matchDone"
			@product = "product"
			@finish = "finish"
			@back = "back"
			@backToColors = "backToColors"
			@backToProduct = "backToProduct"
			:data = "dataSent"
			:itemSelected = "itemSelected"
			:color = "colorSelected"
		></component>
	</transition>

	<div 
		class="c-wave--wrapper--bottom c-wave--wrapper" 
		:class="{
			state1 : waveState1, 
			state2 : waveState2, 
			state3 : waveState3, 
			state4 : waveState4,
			state5 : waveState5,
			state6 : waveState6,
			state7 : waveState7,
			state8 : waveState8,
			stateReset : waveStateReset
		}"
	>
		<div class="c-wave"></div>
	</div>

  </main>
</template>

<script>
import Landing from '~/components/Landing.vue'
import Cards from '~/components/Cards.vue'
import Match from '~/components/Match.vue'
import Colors from '~/components/Colors.vue'
import Product from '~/components/Product.vue'
import Finish from '~/components/Finish.vue'

export default {
  components: {
  	Landing,
  	Cards,
  	Match,
  	Colors,
  	Product,
  	Finish
  },
  data(){
  	return{
  		component: 'Landing',
  		waveState1: false,
  		waveState2: false,
  		waveState3: false,
  		waveState4: false,
  		waveState5: false,
  		waveState6: false, 
  		waveState7: false,
  		waveState8: false,
  		waveStateReset: false,
  		dataSent: [],
  		colorSelected: '',
  		itemSelected: []
  	}
  },
  methods: {
  	start(){
  		this.waveState1 = true;
  		this.component = "Cards"
  	},
  	likeCard(data){
  		this.waveState6 = false;
  		this.waveState2 = true;
  		this.dataSent = data;
  		this.component = "Match"
  	},
  	matchDone(){
  		this.waveState3 = true;
  		this.component = "Colors"
  		this.waveState1 = false;
  		this.waveState2 = false;
        var _self = this;
  		setTimeout(function(){
  			_self.waveStateReset = true;
  		}, 1000)  		
  	},
  	product(color, data){
  		this.component = "Product"
  		this.waveStateReset = false;
  		this.waveState3 = false;
  		this.waveState8 = false;
  		this.waveState1 = true;
  		this.colorSelected = color;
  		this.itemSelected = data;
  	},
  	finish(){
  		this.waveState7 = true;
  		this.component = "Finish"
  	},
  	back(){
  		this.component = "Cards"
  		this.waveState3 = false;
  		this.waveStateReset = false;
  		this.waveState8 = false;
  		this.waveState1 = true;
  	},
  	backToColors(){
  		this.waveState8 = true;
  		this.component = "Colors"
  	},
  	backToProduct(){
		this.component = "Product"
  		this.waveState7 = false;
  		this.waveState1 = true;
  	}
  }
}
</script>

<style lang="scss">
	@import "~/assets/scss/variables/_utils.scss";

	.c-wave{
		  background: url(../assets/images/wave-full.png) repeat-x; 
		  position: absolute;
		  width: 3500px;
		  animation: wave 7s cubic-bezier( 0.36, 0.45, 0.63, 0.53) infinite;
		  transform: translate3d(0, 0, 0);
		  &--wrapper{
			  width:100%;
			  position: fixed;
			  bottom:0;
			  left:0;
			  background: $color-black;
			  transition: all .6s linear;
		  	  .c-wave{
  				height: 450px;	
				width: 4112px;
				top: 0;
		  	  }
			  &--top{
			  	top: 0;
			  	bottom: auto;
			  	transform: translateY(-500px);
		  	    .c-wave{
			  	  background-size: contain;
		  	    }
			  	&.state1{
			  		transform: translateY(-150px);
			  	}
			  	&.state2{
			  		transform: translateY(70px);
			  	}
			  	&.state3{
			  		transform: translateY(600px);
			  		// animation: returnTop 10s;
			  		// animation-delay: 2s;
			  	}
			  	&.state4{
			  		transform: translateY(600px);
			  	}
			  	&.state6{
			  		transform: translateY(600px);
			  		opacity: 0;
			  	}
			  	&.state7{
			  		transform: translateY(520px);
			  	}
			  	&.state8{
			  		transform: translateY(-500px);
			  	}
			  	&.stateReset{
			  		opacity: 0;
			  		transition: none;
			  		transform: translateY(-500px);
			  	}
			  }
			  &--bottom{
			  	transform: translateY(-60px);
			  	&.state1{
			  		transform: translateY(70px);
			  		opacity: 0;
			  	}
			  	// &.state2{
			  	// 	transform: translateY(-500px);
				  // 	top: 0;
				  // 	bottom: auto;
			  	// }
			  	// &.state3{				
			  	// 	transform: translateY(-500px);
				  // 	top: 0;
				  // 	bottom: auto;	
			  	// }
			  	&.state4{
			  		transform: translateY(-150px);
			  		.c-wave{
			  			background-size: contain;
			  		}
			  	}
			  	&.state5{
			  		transform: translateY(470px);
			  	}
			  	&.state6{
			  		transform: translateY(-210px);
		  		    top: 0;
					bottom: auto;
			  		.c-wave{
			  			background-size: contain;
			  		}
			  	}
			  	&.state8{
    				opacity: 1;
			  		transform: translateY(-60px);
			  	}
			  }
		  }
	}

	@keyframes wave {
	  0% {
	    margin-left: 0;
	  }
	  100% {
	    margin-left: -1000px;
	  }
	}

	@keyframes returnTop {
	  0% {
	    opacity: 0;
	  }
	  100% {
	    opacity: 0;
	    transform: translateY(-500px);
	  }
	}

    .fade-enter-active, .fade-leave-active {
	  transition: opacity .5s;
	}
	.fade-enter, .fade-leave-to{
	  opacity: 0;
	}


	.container{
		height: calc(100% - 40px);
	}
	.c-btn{
		text-transform: uppercase;
		font-size: 13px;
		color: $color-black;
		background: $color-white;
		border-radius: 20px;
		text-align: center;
		padding: 14px 20px;
		letter-spacing: 2px;
		display: inline-block;
		&--wraper{
			text-align: center;
			display: block;
			position: relative;
		}
	}
</style>
