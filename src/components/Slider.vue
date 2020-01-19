<template>
<div>
    <transition-group name="fade" tag="div">
      <div v-for="(image,index) in images"
      :key='index'
      v-show="currentIndex == index"
      :style="{backgroundImage: `url(${image})`}"
      class="slide"
      mode="out-in">
          <p>{{ image }}</p>
      </div>
    </transition-group>
    <a class="prev" @click="prev" href='#'>&#10094;</a>
  <a class="next" @click="next" href='#'>&#10095;</a>
  </div>
</template>

<script>
export default {
  name: 'Slider',
  data() {
    return {
      images: [
        'https://cdn.pixabay.com/photo/2015/12/12/15/24/amsterdam-1089646_1280.jpg',
        'https://cdn.pixabay.com/photo/2016/02/17/23/03/usa-1206240_1280.jpg',
        'https://cdn.pixabay.com/photo/2015/05/15/14/27/eiffel-tower-768501_1280.jpg',
        'https://cdn.pixabay.com/photo/2016/12/04/19/30/berlin-cathedral-1882397_1280.jpg'
        ],
      timer: null,
      currentIndex: 0,
    }
  },

  props: {
    delay: {
      type: Number,
      default: 4000
    }
  },

  
    mounted: function() {
      this.startSlide();
    },
  
    methods: {
      startSlide: function() {
        this.timer = setInterval(this.next, this.delay);
      },
  
      next: function() {
        this.currentIndex += 1;
        if(this.currentIndex >= this.images.length) {
          this.currentIndex=0;
        }
      },
      prev: function() {
        this.currentIndex -= 1;
        if(this.currentIndex < 0) {
          this.currentIndex = this.images.length - 1;
        }
      }
    },
  
    computed: {
      // currentImg: function() {
      //   return this.images[Math.abs(this.currentIndex) % this.images.length];
      // }
    }
  
}
</script>

<style lang="scss">
.fade-enter-active,
.fade-leave-active {
  transition: all 3.9s ease;
  //visibility: visible;
  opacity: 1;
}

.fade-enter,
.fade-leave-to {
  //visibility: hidden;
  opacity: 0;
}

.slide {
  min-height: 40rem;
  width: 100%;
  background-size: cover;
  position: absolute;

  > p {
    margin: 0;
  }
}

img {
height:600px;
width:100%
  }

.prev, .next {
  cursor: pointer;
  position: absolute;
  top: 40%;
  width: auto;
  padding: 16px;
  color: white;
  font-weight: bold;
  font-size: 18px;
  transition: 0.7s ease;
  border-radius: 0 4px 4px 0;
  text-decoration: none;
  user-select: none;
  background-color: rgba(0,0,0,0.4);
}

/* Position the "next button" to the right */
.next {
  right: 10px;
}

.prev {
  left: 10px;
}

/* On hover, add a black background color with a little bit see-through */
.prev:hover, .next:hover {
  background-color: rgba(0,0,0,0.9);
}
</style>
