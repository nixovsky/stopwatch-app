<template>
    <div class="stopwatches">
        <div class="stopwatch">
            <span class="stopwatch__time">{{time}}</span>
        </div>
        <div class="stopwatch__control">
            <button v-if="isPlay" class="pause"></button>
            <button v-else class="play"></button>
            <button class="stop"></button>
        </div>
    </div>
</template>

<script>

export default {
    data() {
        return{
            time: "10:10:100",
            isPlay: false,
        }   
    },
}
</script>

<style>
    .stopwatches{
        width: 225px;
        height: 120px;
        background: #696969;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        position: relative;
        margin: 15px 15px;
        position: relative;
    }
    .stopwatches::after{
        content: '';
        position: absolute;
        width: 100%;
        height: 2px;
        top: 50%;
        left: 0;
        background: white;
    }
    .stopwatch{
        margin-bottom: 40px;
    }
    .stopwatch__time{
        font-weight: 400;
        font-size: 20px;
    }
    .stopwatch__control button{
        background: 0;
        border: 0;
        color: white;
        position: relative;
        width: 20px;
        height: 20px;
        margin-right: 20px;
    }
    .stopwatch__control button:last-child{
        margin-right: 0;
    }
    .play::before{
        content: '';
        position: absolute;
        width: 0;
        height: 0;
        border-top: 10px solid transparent;
        border-left: 20px solid white;
        border-bottom: 10px solid transparent;
        left: 0;
        top: 0;
        cursor: pointer;
    }
    .pause::after{
        content: '';
        position: absolute;
        width: 7px;
        height: 100%;
        top: 0;
        right: 0;
        background: white;
        cursor: pointer;
    }
    .pause::before{
        content: '';
        position: absolute;
        width: 7px;
        height: 100%;
        top: 0;
        left: 0;
        background: white;
        cursor: pointer;
    }
    .stop::before{
        content: '';
        position: absolute;
        width: 20px;
        height: 20px;
        top: 0;
        left: 0;
        background: white;
        cursor: pointer;
    }
    .inactive::before{
        content: '';
        position: absolute;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        z-index: 100;
        background: rgba(0, 0, 0, 0.2);
    }
</style>