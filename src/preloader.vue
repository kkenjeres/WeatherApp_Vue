<template>
    <div v-if="show" class="preloader">
        <p>CHECK THE WEATHER</p>
        <div class="lds-ripple"><div></div><div></div></div>
    </div>
</template>

<script> 
export default {
    name: 'preloader',
    data(){
        return{
            show: true
        }
    },
    mounted(){
        this.showToggle()
     },
        methods:{
            showToggle(){
                setTimeout(() => {
                    this.show = false
                }, 3000)
            }
       }
}
</script>

<style>

.preloader{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    position: absolute;
    width: 100%;
    height: 100%;
    background: linear-gradient(rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.8)),
    url('../src/assets/img/statya.jpg') bottom no-repeat,
    url('../src/assets/img/triangle.jpg');
}
p{
    margin-bottom: 40px;
    font-size: 72px;
    font-weight: medium;
    background: #ffffff;
}
.lds-ripple {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-ripple div {
  position: absolute;
  border: 4px solid #fff;
  opacity: 1;
  border-radius: 50%;
  animation: lds-ripple 1s cubic-bezier(0, 0.2, 0.8, 1) infinite;
}
.lds-ripple div:nth-child(2) {
  animation-delay: -0.5s;
}
@keyframes lds-ripple {
  0% {
    top: 36px;
    left: 36px;
    width: 0;
    height: 0;
    opacity: 1;
  }
  100% {
    top: 0px;
    left: 0px;
    width: 72px;
    height: 72px;
    opacity: 0;
  }
}
</style>