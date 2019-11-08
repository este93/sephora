<template>
	<div class="c-cards">
		<div class="c-cards__count"><span>1</span>/<span>3</span></div>
        <h1 class="c-cards__title">je choisis mon fini ultra pigmenté</h1>
		<div class="c-cards__nav">
			<div class="c-cards__nav--left">
				<h3 class="c-cards__nav__title" v-html="activeSubtitle"></h3>
				<div class="c-cards__nav__dots">
					<span class="c-cards__nav__dots__item" id="item1" :data-id="activeDot"></span>
					<span class="c-cards__nav__dots__item" id="item2" :data-id="activeDot"></span>
					<span class="c-cards__nav__dots__item" id="item3" :data-id="activeDot"></span>
					<span class="c-cards__nav__dots__item" id="item4" :data-id="activeDot"></span>
					<span class="c-cards__nav__dots__item" id="item5" :data-id="activeDot"></span>
				</div>
			</div>
		</div>

    	<transition name="fade">
	        <div
	        v-if="isShowing"
	        class="wrapper"
	        >
		        <GameCard
		          v-for="(card, index) in cards"
		          :key="index"
		          :index="index"
		          :card="card"
		          :data-index = "index + dataIndex"
		          @hideCard="removeCardFromDeck"
		        />   
	        </div>
		</transition>

		<div class="c-cards__like" @click="likeCard">je valide cette teinte</div>

	</div>
</template>

<script>
import GameCard from "@/components/card-item";

export default {
  components: {
    GameCard
  },

  data() {
    return {
      counter: 0,
      isShowing: true,
      dataIndex: 1,
      activeDot: 1,
      activeSubtitle: "CREAM LIP<br>STAIN MAT SANS TRANSFERT",
      cards: [
      	{
      		"title" : 'Mat',
      		'image' : 'mat1.jpg',
      		'category' : 'Cream lip stain',
      		'items' : [
      			{
      				'title' : 'rouge/ Bordeaux',
      				'image' : 'mat1.jpg',
  					'category' : 'Cream lip stain',
  					'parent' : 'Mat',
  					'price' : '10,99€',
		      		'colors': [
				        {
				          'id': 1,
				          'color': '#d32a33',
				          'number': '01'
				        },
				        {
				          'id': 2,
				          'color': '#973c45',
				          'number': '17'
				        },
				        {
				          'id': 3,
				          'color': '#683736',
				          'number': '27'
				        },
				        {
				          'id': 4,
				          'color': '#8b433f',
				          'number': '42'
				        },
				        {
				          'id': 5,
				          'color': '#71443b',
				          'number': '43'
				        },
				        {
				          'id': 6,
				          'color': '#a32143',
				          'number': '94'
				        },
				        {
				          'id': 7,
				          'color': '#9a434b',
				          'number': '96'
				        },
				        {
				          'id': 8,
				          'color': '#82353a',
				          'number': '97'
				        },
				        {
				          'id': 9,
				          'color': '#64363d',
				          'number': '99'
				        }
				    ]
      			},
      			{
      				'title' : 'rose/ bois de rose/ prune',
      				'image' : 'mat2.jpg',
  					'category' : 'Cream lip stain',
  					'parent' : 'Mat',
  					'price' : '10,99€',
		      		'colors': [
				        {
				          'id': 1,
				          'color': '#f34871',
				          'number': '03'
				        },
				        {
				          'id': 2,
				          'color': '#9b4857',
				          'number': '04'
				        },
				        {
				          'id': 3,
				          'color': '#f29e9a',
				          'number': '05'
				        },
				        {
				          'id': 4,
				          'color': '#d28797',
				          'number': '06'
				        },
				        {
				          'id': 5,
				          'color': '#c67893',
				          'number': '07'
				        },
				        {
				          'id': 6,
				          'color': '#ca808b',
				          'number': '13'
				        },
				        {
				          'id': 7,
				          'color': '#9d4c5e',
				          'number': '14'
				        },
				        {
				          'id': 8,
				          'color': '#853c55',
				          'number': '16'
				        },
				        {
				          'id': 9,
				          'color': '#b3867e',
				          'number': '23'
				        },
				        {
				          'id': 10,
				          'color': '#7e4343',
				          'number': '24'
				        },
				        {
				          'id': 11,
				          'color': '#bf7393',
				          'number': '38'
				        }
				    ]
      			}
      		],
      	},
      	{
      		"title" : 'Metallique',
      		'image' : 'metaliique1.jpg',
      		'category' : 'Cream lip stain',
      		'items' : [
      			{
      				'title' : 'Metallique',
      				'image' : 'metaliique.jpg',
      				'category' : 'Cream lip stain',
  					'parent' : 'Metallique',
  					'price' : '10,99€',
		      		'colors': [
				        {
				          'id': 1,
				          'color': '#831d2b',
				          'number': '58'
				        },
				        {
				          'id': 2,
				          'color': '#a6625c',
				          'number': '61'
				        },
				        {
				          'id': 3,
				          'color': '#ecaf6c',
				          'number': '63'
				        },
				        {
				          'id': 4,
				          'color': '#ad4950',
				          'number': '64'
				        },
				        {
				          'id': 5,
				          'color': '#cf6e5d',
				          'number': '106'
				        },
				        {
				          'id': 6,
				          'color': '#d24e53',
				          'number': '107'
				        },
				        {
				          'id': 7,
				          'color': '#f3c8c3',
				          'number': '109'
				        },
				        {
				          'id': 8,
				          'color': '#f15259',
				          'number': '110'
				        },
				        {
				          'id': 9,
				          'color': '#e2b3a3',
				          'number': '113'
				        },
				        {
				          'id': 10,
				          'color': '#efa293',
				          'number': '115'
				        },
				    ]
      			},
      		],
      	},
      	{
      		"title" : 'Duochrome',
      		'image' : 'duochrome.jpg',
      		'category' : 'Cream lip stain',
      		'items' : [
      			{
      				'title' : 'Duochrome',
      				'image' : 'duochrome.jpg',
      				'category' : 'Cream lip stain',
  					'parent' : 'Duochrome',
  					'price' : '10,99€',
		      		'colors': [
				        {
				          'id': 1,
				          'color': '#82506d',
				          'number': '123'
				        },
				        {
				          'id': 2,
				          'color': '#8b4d58',
				          'number': '124'
				        },
				        {
				          'id': 3,
				          'color': '#b65762',
				          'number': '125'
				        },
				        {
				          'id': 4,
				          'color': '#495f6c',
				          'number': '126'
				        },
				        {
				          'id': 5,
				          'color': '#876248',
				          'number': '127'
				        },
				        {
				          'id': 6,
				          'color': '#9f556a',
				          'number': '128'
				        },
				        {
				          'id': 7,
				          'color': '#87537d',
				          'number': '129'
				        },
				        {
				          'id': 8,
				          'color': '#68667c',
				          'number': '130'
				        },
				        {
				          'id': 9,
				          'color': '#9d5d68',
				          'number': '131'
				        }
				    ]
      			},
      		],
      	},
      	{
      		"title" : 'Brillant',
      		'image' : 'brillant.jpg',
      		'category' : 'Cream lip shine',
      		'items' : [
      			{
      				'title' : 'Brillant',
      				'image' : 'brillant.jpg',
      				'category' : 'Cream lip shine',
  					'parent' : 'Brillant',
  					'price' : '10,99€',
		      		'colors': [
				        {
				          'id': 1,
				          'color': '#9d5d53',
				          'number': '01'
				        },
				        {
				          'id': 2,
				          'color': '#7e454f',
				          'number': '03'
				        },
				        {
				          'id': 3,
				          'color': '#8d5d59',
				          'number': '04'
				        },
				        {
				          'id': 4,
				          'color': '#68232d',
				          'number': '05'
				        },
				        {
				          'id': 5,
				          'color': '#b72b30',
				          'number': '06'
				        },
				        {
				          'id': 6,
				          'color': '#6f1414',
				          'number': '07'
				        },
				        {
				          'id': 7,
				          'color': '#93040f',
				          'number': '08'
				        },
				        {
				          'id': 8,
				          'color': '#9d043d',
				          'number': '09'
				        },
				        {
				          'id': 9,
				          'color': '#810a4b',
				          'number': '10'
				        },
				        {
				          'id': 10,
				          'color': '#460d21',
				          'number': '11'
				        },
				        {
				          'id': 11,
				          'color': '#c57c70',
				          'number': '12'
				        },
				        {
				          'id': 12,
				          'color': '#bb5257',
				          'number': '13'
				        },
				        // {
				        //   'id': 13,
				        //   'color': '#682228',
				        //   'number': '14'
				        // },
				        // {
				        //   'id': 14,
				        //   'color': '#451c32',
				        //   'number': '15'
				        // },
				        // {
				        //   'id': 15,
				        //   'color': '#d75e5a',
				        //   'number': '16'
				        // },
				        // {
				        //   'id': 16,
				        //   'color': '#8a2f8d',
				        //   'number': '17'
				        // },
				        // {
				        //   'id': 17,
				        //   'color': '#883f38',
				        //   'number': '18'
				        // },
				        // {
				        //   'id': 18,
				        //   'color': '#c22d54',
				        //   'number': '19'
				        // },
				        // {
				        //   'id': 19,
				        //   'color': '#c31c1f',
				        //   'number': '20'
				        // },
				        // {
				        //   'id': 20,
				        //   'color': '#830221',
				        //   'number': '21'
				        // }
				    ]
      			},
      		],
      	},
      	{
      		"title" : 'Brillant Metallique',
      		'image' : 'card5.jpg',
      		'category' : 'Cream lip shine',
      		'items' : [
      			{
      				'title' : 'Brillant Metallique',
      				'image' : 'brillantMetallique.jpg',
      				'category' : 'Cream lip shine',
  					'parent' : 'Brillant Metallique',
  					'price' : '10,99€',
		      		'colors': [
				        {
				          'id': 1,
				          'color': '#d75377',
				          'number': '22'
				        },
				        {
				          'id': 2,
				          'color': '#bf3e38',
				          'number': '23'
				        },
				        {
				          'id': 3,
				          'color': '#7d4548',
				          'number': '24'
				        },
				        {
				          'id': 4,
				          'color': '#de863f',
				          'number': '25'
				        },
				        {
				          'id': 5,
				          'color': '#a60016',
				          'number': '26'
				        },
				        {
				          'id': 6,
				          'color': '#d85166',
				          'number': '27'
				        },
				        {
				          'id': 7,
				          'color': '#de8c57',
				          'number': '28'
				        },
				        {
				          'id': 8,
				          'color': '#fd788b',
				          'number': '29'
				        },
				        {
				          'id': 9,
				          'color': '#e95350',
				          'number': '30'
				        },
				        {
				          'id': 10,
				          'color': '#b6317f',
				          'number': '31'
				        }
				    ]
      			},
      		],
      	}
      ]
    };
  },

  methods: {
  	likeCard(){
  		this.$emit('likeCard', this.cards[this.activeDot - 1]);
  	},
    removeCardFromDeck(as) {
  	  this.activeDot++;
      this.counter ++;
      this.dataIndex --;
      if(this.activeDot > 3){
      	this.activeSubtitle = "CREAM LIP<br>SHINE ULTRA BRILLANT";
      }else{
      	this.activeSubtitle = "CREAM LIP<br>STAIN MAT SANS TRANSFERT";
      }
      if(this.counter == this.cards.length){
        this.isShowing = false;
        this.counter = 0;
        this.dataIndex = 1;
        this.activeDot = 1;
      	this.activeSubtitle = "CREAM LIP<br>STAIN MAT SANS TRANSFERT";
        setTimeout(() => {
          this.isShowing = true;
        }, 50);
      }

    }
  }

};
</script>

<style lang="scss">
	@import "~/assets/scss/variables/_utils.scss";

	.c-cards{
	    padding-top: 10px;
	    position: relative;
	    -ms-touch-action: pan-y;
	    touch-action: pan-y;
	    .wrapper{
	        position: relative;
	        margin: 0 35px;
	        background: $color-gray;
	        border-radius: 12px;
			padding: 22px 24px 7.3vH 24px;
  			box-shadow: 0px 0px 34.4px 8.6px rgba(0, 0, 0, 0.19);
  			z-index: 1;
	    }
	    &__count{
	    	border-radius: 15px;
	    	background: $color-white;
	    	text-align: center;
	    	font-size: 10px;
	    	max-width: 33px;
	    	margin: auto;
	    	margin-bottom: 6px;
	    	padding: 8px 0;
	    	span{
	    		margin: 0 1px;
	    	}
	    }
		&__title{
			text-transform: uppercase;
			color: $color-primary;
			font-size: 20px;
			line-height: 24px;
			font-family: AvalonBoldOblique;
			text-align: center;
			margin: 0 auto 13px auto;
			position: relative;
			z-index: 1;
			max-width: 200px;
			span{
				color: $color-black;
			}
		} 
	    &__nav{
			position: relative;
			z-index: 1;
			padding: 0 30px;
			text-align: center;
			margin-bottom: 16px;
			&__title{
				color: $color-white;
				text-transform: uppercase;
				font-family: AvalonBold;
				font-size: 12px;
				line-height: 15px;
				padding: 0 11px;
				margin: auto;
				margin-bottom: 5px;
			}
			&__dots{
				&__item{
					width: 8px;
					height: 8px;
					border-radius: 100%;
					background: $color-white;
					margin: 0 1.5px;
					display: inline-block;
					opacity: .3;
					&#item1[data-id="1"]{
						opacity: 1;
					}
					&#item2[data-id="2"]{
						opacity: 1;
					}
					&#item3[data-id="3"]{
						opacity: 1;
					}
					&#item4[data-id="4"]{
						opacity: 1;
					}
					&#item5[data-id="5"]{
						opacity: 1;
					}
				}
			}
	    }  
	    &__like{	    	
			background: $color-black;
			text-align: center;
			color: $color-white;
			border-radius: 20px;
			text-transform: uppercase;
			font-size: 13px;
			padding: 13px 10px;
			letter-spacing: 2px;
		    width: 56%;
			margin: auto;
			position: relative;
			top: -25px;
			z-index: 1;
	    }
	}
</style>