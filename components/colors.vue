<template>
	
	<div class="c-colors" :class="{ multiple: data.items.length > 1 }">	
    <div class="c-cards__count"><span>2</span>/<span>3</span></div>	
    <h1 class="c-colors__title">
      <span>{{ data.category }}</span>
      {{ data.title }}
    </h1>
    <div v-if="data.items.length > 1" class="c-colors__multiple">
      <div 
        class="c-colors__multiple__item" 
        v-for="(item, index) in data.items"
        :key="index"
      >
        <h3 class="c-colors__multiple__title"><span>{{ item.title }}</span></h3>
        <div class="c-colors__multiple__img">          
          <img :src="getImgUrl(item.image)" alt="">  
        </div>
        <ul class="c-colors__list">
            <li 
              class="c-colors__list__item" 
              v-for="color in item.colors"
              :style="`background:` + color.color"
              @click="selectColor(color.id, item)"
              :class="{highlight : color.id == colorSelected && selectedItem.colors[color.id - 1].number == color.number}"
            >
              {{ color.number }}
          </li>
        </ul>
      </div>
    </div>
    <div v-else class="c-colors--wrapper">
      <div class="c-colors__img">
        <img :src="getImgUrl(data.items[0].image)" alt="">  
      </div>
      <ul class="c-colors__list">
          <li 
            class="c-colors__list__item" 
            v-for="color in data.items[0].colors"
            :style="`background:` + color.color"
            @click="selectColor(color.id, data.items[0])"
            :class="{highlight : color.id == colorSelected}"
          >
            {{ color.number }}
        </li>
      </ul>
    </div>
    

    <div class="b-valider">
      <div class="b-valider__item" @click="back"><span></span>Retour</div>
      <div class="b-valider__item" @click="selectProduct" v-if="colorSelected">Valider<span></span></div>
    </div>
	</div>

</template>


<script>

export default {	
  props: ['data'],
  data(){
    return{
      colorSelected: false,
      selectedItem: []    
    }
  },
  methods: {
    getImgUrl(img) {
      return require('@/assets/images/'+img)
    },
    selectColor(color, item){
      this.selectedItem = item;
      this.colorSelected = color;
    },
    back(){
      this.$emit('back');
    },
    selectProduct(){
      if(this.colorSelected){
        this.$emit('product', this.colorSelected - 1, this.selectedItem)
      }else{
        alert("Choose color")
      }
    }
  }
}

</script>

<style lang="scss">
  @import "~/assets/scss/variables/_utils.scss";
  .b-valider{
    display: flex;
    justify-content: space-between;
    color: $color-white;
    position: fixed;
    bottom: 15px;
    left: 0;
    right: 0;
    z-index: 1;
    padding: 0 19px;
    &__item{
      font-size: 12.5px;
      &:nth-child(2){
        span{
          margin-right: 0;
          margin-left: 10px;
          transform: rotate(180deg);
        }
      }
      span{
        border-radius: 100%;
        border: 2px solid $color-white;
        width: 30px;
        height: 30px;
        display: inline-block;
        background: url(../assets/images/arrow.png) no-repeat center center; 
        background-size: 8.5px 13px;
        vertical-align: middle;
        margin-right: 10px;   
      }
    }
  }
  
  .c-colors{
    padding: 15px 0;
    height: 100%;
    &.multiple{
      padding: 10px 0 0 0;
      .c-colors__title{
        margin-bottom: -3px;
      }
      .c-colors__list{
        white-space: normal;
      }
    }
    .c-cards__count{
      background: $color-gray;
      position: relative;
    }
    &--wrapper{
      padding: 0 46px;
    }
    &__title{
      text-transform: uppercase;
      color: $color-primary;
      font-size: 20px;
      line-height: 24px;
      font-family: AvalonBoldOblique;
      text-align: center;
      max-width: 250px;
      margin: 0 auto 10px auto;
      position: relative;
      span{
        color: $color-black;
      }
    } 
    &--content{
      padding: 0 45px;
    }
    &__img{
      margin-bottom: 7px;
      img{
        border-radius: 30px;
      }
    }
    &__list{
      padding: 0 7px;
      &__item{
        text-align: center;
        width: 31px;
        line-height: 31px;
        border-radius: 100%;
        background: black;
        color: $color-white;
        font-family: AvalonBold;
        font-size: 12px;
        display: inline-block;
        margin: 4px 3px;
        border: 2px solid transparent;
        z-index: 1;
        position: relative;
        &.highlight{
          border-color: $color-black;
        }
      }
    }
    &__multiple{      
      overflow: auto;
      white-space: nowrap;
      -webkit-overflow-scrolling: touch;
      &::-webkit-scrollbar {
        display: none;
      }
      &__item{
        display: inline-block;
        vertical-align: top;
        max-width: 82%;
        margin-right: 9px;
        &:first-child{
          margin-left: 9px;
        }
      }
      &__img{
        border-radius: 25px;
        margin-bottom: 3px;
        overflow: hidden;
      }
      &__title{
        text-transform: uppercase;
        font-size: 10px;
        z-index: 1;
        position: relative;
        top: 29px;
        left: 14px;
        letter-spacing: -0.2px;
        span{
          background: $color-gray;
          padding: 9px 18px 6px 19px;
          border-radius: 15px;
        }
      }
    }
  }
</style>