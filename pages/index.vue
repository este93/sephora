<template>
  <main class="container">

  	<div class="horizontal" v-if="isHorizontal"></div>

	<div 
		class="c-wave--wrapper--top c-wave--wrapper" 
		:class="{
			state1 : waveState1, 
			state2 : waveState2, 
			state3 : waveState3, 
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
	  		waveState5: false,
	  		waveState6: false, 
	  		waveState7: false,
	  		waveState8: false,
	  		waveStateReset: false,
	  		dataSent: [],
	  		colorSelected: '',
	  		itemSelected: [],
	  		isHorizontal: false
	  	}
    },
	mounted() {
	  this.$nextTick(()=>{
	    window.addEventListener('resize', this.detectOrientationChange)
	  })
	},
    created(){
	    if (process.browser){
			this.detectOrientationChange();
	    }
    },
    beforeDestroy() {
	   window.removeEventListener("resize", this.detectOrientationChange);
	},
    methods: {
		detectOrientationChange(e) {
		    if (window.matchMedia("(orientation: landscape)").matches) {
			    this.isHorizontal = true;
			}else{
				this.isHorizontal = false;
			}
		},
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
		  background: url(../assets/images/wave.svg) repeat-x; 
		  position: absolute;
		  width: 4800px;
		  height: 480px;
		  top: 0;
		  animation: wave 7s cubic-bezier( 0.36, 0.45, 0.63, 0.53) infinite;
		  transform: translate3d(0, 0, 0);
		  &--wrapper{
			  width:100%;
			  position: fixed;
			  bottom:0;
			  left:0;
			  background: $color-black;
			  transition: all 1s ease-out;
		  	  .c-wave{
		  	  }
			  &--top{
			  	top: 0;
			  	bottom: auto;
			  	transform: translateY(-500px);
		  	    .c-wave{
			  	  background-size: contain;
		  	    }
			  	&.state1{
			  		transform: translateY(-180px);
			  	}
			  	&.state2{
			  		transform: translateY(70px);
			  	}
			  	&.state3{
			  		transform: translateY(600px);
			  	}
			  	&.state6{
			  		transform: translateY(600px);
			  		opacity: 0;
			  	}
			  	&.state7{
			  		transition: transform 2s ease-out;
			  		transform: translateY(75vH);
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
			  	transform: translateY(-90px);
			  	&.state1{
			  		transform: translateY(70px);
			  		opacity: 0;
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
			  		transform: translateY(-90px);
			  	}
			  }
		  }
	}

	@keyframes wave {
	  0% {
	    margin-left: 0;
	  }
	  100% {
	    margin-left: -1200px;
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
	  transition: opacity .4s;
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

	.horizontal{
		background: url(../assets/images/horizontal.jpg) center center no-repeat;
		background-size: cover;     
		position: fixed;
	    top: 0;
	    left: 0;
	    width: 100%;
	    height: 100%;
	    z-index: 10;
	}
</style>
