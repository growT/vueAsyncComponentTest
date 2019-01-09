<template>
   <div class="tx-vue-loading" :style="{background: ['rgba(255,255,255,' + maskOpcity + ')']}" >
        <div class="picLoading" :class="size">
            <div class="rect1" :style="{backgroundColor: color}"></div>
            <div class="rect2" :style="{backgroundColor: color}"></div>
            <div class="rect3" :style="{backgroundColor: color}"></div>
            <div class="rect4" :style="{backgroundColor: color}"></div>
            <div class="rect5" :style="{backgroundColor: color}"></div>
        </div>
    </div>
</template>
<script>

export default {
    name:'tx-vue-loading', 
    data() {
        return {
            
        }
    },
    props:{
        color:{
            type:String,
            default: '#ff6600'
        },
        size:{
            type:String,
            default:'middle',
        },
        maskOpcity:{
            type:Number,
            default: .8
        }
    }
}
</script>

<style scoped>
.tx-vue-loading{
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
}
.picLoading {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 50px;
    text-align: center;
    font-size: 10px;
    transform: translate(-50%,-50%);
}
.big {
    height: 90px;
}
.middle {
    height: 60px;
}
.small {
    height: 30px;
}
.picLoading > div {
    /* background-color: #ff6600; */
    height: 100%;
    width: 6px;
    display: inline-block;
    -webkit-animation: stretchdelay 1.2s infinite ease-in-out;
    animation: stretchdelay 1.2s infinite ease-in-out;
}
.picLoading .rect2 {
    -webkit-animation-delay: -1.1s;
    animation-delay: -1.1s;
}
.picLoading .rect3 {
    -webkit-animation-delay: -1.0s;
    animation-delay: -1.0s;
}
.picLoading .rect4 {
    -webkit-animation-delay: -0.9s;
    animation-delay: -0.9s;
}
.picLoading .rect5 {
    -webkit-animation-delay: -0.8s;
    animation-delay: -0.8s;
}

@-webkit-keyframes stretchdelay {
    0%, 40%, 100% { -webkit-transform: scaleY(0.4) } 
    20% { -webkit-transform: scaleY(1.0) }
}

@keyframes stretchdelay {
    0%, 40%, 100% {
        transform: scaleY(0.4);
        -webkit-transform: scaleY(0.4);
    }  20% {
        transform: scaleY(1.0);
        -webkit-transform: scaleY(1.0);
    }
}
</style>
