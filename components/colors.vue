<template>
	
	<div class="c-colors" :class="{ multiple: data.items.length > 1 }">		
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
        <h3 class="c-colors__multiple__title">{{ item.title }}</h3>
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
      <div class="b-valider__item" @click="selectProduct">Valider<span></span></div>
    </div>
	</div>

</template>


<script>

export default {	
  props: ['data'],
  data(){
    return{
      colorSelected: undefined,
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
      this.$emit('product', this.colorSelected - 1, this.selectedItem)
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
    position: absolute;
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
      padding: 15px 0 0 18px;
      .c-colors__list{
        white-space: normal;
      }
    }
    &--wrapper{
      padding: 0 46px;
    }
    &__title{
      text-transform: uppercase;
      color: $color-primary;
      font-size: 25px;
      line-height: 25px;
      line-height: 30px;
      font-family: AvalonBoldOblique;
      text-align: center;
      margin-bottom: 13px;
      span{
        color: $color-black;
        display: block;
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
      max-width: 215px;
      margin: auto;
      &__item{
        text-align: center;
        width: 29px;
        line-height: 29px;
        border-radius: 100%;
        background: black;
        color: $color-white;
        font-family: AvalonBold;
        font-size: 10.5px;
        display: inline-block;
        margin: 4px 2px;
        border: 1px solid transparent;
        &.highlight{
          border-color: $color-black;
        }
      }
    }
    &__multiple{      
      overflow: auto;
      white-space: nowrap;
      &__item{
        display: inline-block;
        max-width: 75%;
        margin-right: 18px;
      }
      &__img{
        border-radius: 20px;
        margin-bottom: 7px;
        overflow: hidden;
      }
      &__title{
        text-transform: uppercase;
        text-align: center;
        background: $color-gray;
        font-size: 12.5px;
        padding: 7px;
        border-radius: 15px;
        width: 77%;
        margin: auto;
        margin-bottom: -10px;
        z-index: 1;
        position: relative;
      }
    }
  }
</style>