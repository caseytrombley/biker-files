<template>
<!--  <b-button :class="{ 'animated-button': animated }">-->
<!--    <slot />-->
<!--  </b-button>-->

  <div class="box">
    <b-button class="btn">
      <slot />
    </b-button>
  </div>
</template>

<script>
export default {
  name: 'BaseButton',
  data() {
    return {
      isAnimating: false,
    };
  },
  props: {
    animated: {
      type: Boolean,
      default: false
    }
  },
};
</script>

<style lang="scss" scoped>
.box {
  width: fit-content;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: $color-primary;
  border-radius: 50px;
}

.btn {
  padding: 0;
  color: #ffffff;
  transition: all 0.5s;
  position: relative;
  font-weight: 600;
  line-height: 50px;
  height: 50px;
  text-align: center;
  width: 250px;
  cursor: pointer;
  border-radius: 50px;
  background-color: $color-primary;

  &:hover,
  &:active,
  &:focus {
    color: #ffffff;
    background-color: $color-primary;
  }
}

.btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
  background-color: rgba(255,255,255,0.1);
  border-radius: 50px;
  transition: all 0.3s;
}
.btn:hover::before {
  opacity: 0 ;
  transform: scale(0.5,0.5);
}
.btn::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
  opacity: 0;
  transition: all 0.3s;
  transform: scale(1.2,1.2);
}
.btn:hover::after {
  opacity: 1;
  transform: scale(1,1);
}


/* Button styles */
//.animated-button {
//  padding: 12px 24px;
//  font-size: 16px;
//  font-weight: bold;
//  color: #fff;
//  background-color: $color-primary;
//  border: none;
//  border-radius: 50px;
//  cursor: pointer;
//  position: relative;
//  overflow: hidden;
//  z-index: 1;
//}
//
///* Animation shake keyframes */
//@keyframes shake {
//  0% { transform: translateX(0); }
//  25% { transform: translateX(-5px) rotateZ(-5deg); }
//  50% { transform: translateX(5px) rotateZ(5deg); }
//  75% { transform: translateX(-3px) rotateZ(-3deg); }
//  100% { transform: translateX(3px) rotateZ(3deg); }
//}
//
///* Hover animation */
//.animated-button:hover {
//  animation: shake 0.3s infinite;
//}

</style>
