<template>
  <div
    v-if="isShowing"
    ref="interactElement"
    class="itemCard"
    :style="{ transform: transformString }"
  >
    <div class="card">
      <div class="card__title">
        {{ card.title }}
      </div>  
      <div class="card__img">
        <div class="card__overlay">
          <div></div>
          <img :src="getImgUrl(card.image)" alt="">            
        </div>
      </div>    
    </div>
  </div>
</template>

<script>
import interact from "interactjs";
const ACCEPT_CARD = "cardAccepted";
const REJECT_CARD = "cardRejected";

export default {
  static: {
    interactMaxRotation: 5,
    interactOutOfSightXCoordinate: 500,
    interactOutOfSightYCoordinate: 600,
    interactYThreshold: 150,
    interactXThreshold: 45
  },

  props: ['card', 'index'],

  data() {
    return {
      isShowing: true,
      isInteractAnimating: true,
      isInteractDragged: null,
      interactPosition: {
        x: 0,
        y: 0,
        rotation: 0
      }
    };
  },

  computed: {
    transformString() {
      if (!this.isInteractAnimating || this.isInteractDragged) {
        const { x, y, rotation } = this.interactPosition;
        return `translate3D(${x}px, 0, 0) rotate(${rotation}deg)`;
      }

      return null;
    }
  },

  mounted() {
    const element = this.$refs.interactElement;

    interact(element).draggable({

      // axis: "x",   // allowing vertical scroll

      onstart: () => {
        this.isInteractAnimating = false;
      },

      onmove: event => {
        const {
          interactMaxRotation,
          interactXThreshold
        } = this.$options.static;
        const x = this.interactPosition.x + event.dx;
        const y = 0;
        let rotation = interactMaxRotation * (x / interactXThreshold);

        if (rotation > interactMaxRotation) rotation = interactMaxRotation;
        else if (rotation < -interactMaxRotation)
          rotation = -interactMaxRotation;

        this.interactSetPosition({ x, y, rotation });
      },

      onend: () => {
        const { x } = this.interactPosition;
        const { interactXThreshold, interactYThreshold } = this.$options.static;
        this.isInteractAnimating = true;

        if (x > interactXThreshold) this.playCard(REJECT_CARD);
        else if (x < -interactXThreshold) this.playCard(REJECT_CARD);
        else this.resetCardPosition();
      }
    });
  },

  beforeDestroy() {
    interact(this.$refs.interactElement).unset();
  },

  methods: {
    getImgUrl(img) {
      return require('@/assets/images/'+img)
    },
    hideCard() {
      this.$emit("hideCard", this.card);
    },

    playCard(interaction) {
      const {
        interactOutOfSightXCoordinate,
        interactOutOfSightYCoordinate,
        interactMaxRotation
      } = this.$options.static;

      this.interactUnsetElement();

      switch (interaction) {
        case ACCEPT_CARD:
          this.interactSetPosition({
            x: interactOutOfSightXCoordinate,
            rotation: interactMaxRotation
          });
          break;
        case REJECT_CARD:
          this.interactSetPosition({
            x: -interactOutOfSightXCoordinate,
            rotation: -interactMaxRotation
          });
          break;
      }

      this.hideCard();
    },

    interactSetPosition(coordinates) {
      const { x = 0, y = 0, rotation = 0 } = coordinates;
      this.interactPosition = { x, y, rotation };
    },

    interactUnsetElement() {
      interact(this.$refs.interactElement).unset();
      this.isInteractDragged = true;
    },

    resetCardPosition() {
      this.interactSetPosition({ x: 0, y: 0, rotation: 0 });
    }
  }
};
</script>

<style lang="scss">
  @import "~/assets/scss/variables/_utils.scss";

  .itemCard{
    position: relative;
      width: 100%;
    cursor: -webkit-grab;
    cursor: grab;
    -ms-touch-action: pan-y;
    touch-action: pan-y;
    .card{
      transition: transform 2s cubic-bezier(0.175, 0.885, 0.32, 1.275) 0s;
      position: relative;
      -webkit-transform: translateX(0) translateY(0) translateZ(0);
      transform: translateX(0) translateY(0) translateZ(0);
      opacity: 1;
      transition: opacity 2s linear;
      &__title{
        text-align: center;
        text-transform: uppercase;
        font-family: AvalonBoldOblique;
        font-size: 27px;
        min-height: 55px;
      }
      &__overlay{
        display: inline-block;
        position: relative;
        div{
          position: absolute;
          top: 0;
          left: 0;
          width: 100%;
          height: 100%;
          background: $color-gray;
          opacity: 0;
          animation: opacity .5s cubic-bezier( 0.36, 0.45, 0.63, 0.53);
        }
      }
      &__img{
        overflow: hidden;
        text-align: center;
        img{
          display: block;
          max-height: 31vH;
          margin: auto;
          border: 5px solid $color-white;
          border-radius: 20px;
          box-sizing: border-box;
        }        
      }
    }
    &:not([data-index='1']) {
      display: none;
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      margin: auto;
      .card{
        opacity: 0;
        transform: scale(.6);
        transition: all .2s linear;        
      }
      .card__overlay div{
        opacity: 1;
      }
    }
  }

  @keyframes opacity {
    0% {
      opacity: 1;
    }
    100% {
      opacity: 0;
    }
  }
</style>
