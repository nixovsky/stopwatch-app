<template>
    <div class="stopwatches" :class="{inactive: !isPlay}">
        <div class="stopwatch">
            <span class="stopwatch__time">{{time}}</span>
        </div>
        <div class="stopwatch__control">
            <button v-if="isPlay" 
                    @click="pauseTimer" 
                    class="pause"></button>
            <button v-else 
                    @click="startTimer" 
                    class="play"></button>
            <button class="stop"
                    @click="stopTimer"></button>
        </div>
    </div>
</template>

<script>

export default {
    data() {
        return{
            time: "0",
            isPlay: false,
            sec: 0,
            min: 0,
            hour: 0,
            isSec: false,
            isMin: false
        }   
    },
    methods:{
        oneTick(){
            this.sec += 1;
            if (this.sec >= 60){
                this.isSec = true;
                this.sec = 0;
                this.min += 1;
                if (this.min >= 60){
                    this.isMin = true;
                    this.min = 0;
                    this.hour += 1;
                }
            }
            this.setTime();
        },
        setTime() {
            // Валидирует строку вывода таймера
            // если 60 секунд прошли, в вывод добавляются минуты
            // если прошли 60 минут, в вывод добавляются часы
            if(this.isSec && !this.isMin){
                this.time = (this.min > 9 ? this.min : "0" + this.min) + ":" +
                            (this.sec > 9 ? this.sec : "0" + this.sec);
            }
            else if(this.isSec && this.isMin){
                this.time = (this.hour > 9 ? this.hour : "0" + this.hour) + ":" +
                            (this.min > 9 ? this.min : "0" + this.min) + ":" +
                            (this.sec > 9 ? this.sec : "0" + this.sec);
            }
            else{
                this.time = this.sec > 9 ? this.sec : "0" + this.sec;
            }
        },
        startTimer(){
            this.isPlay = !this.isPlay;

            this.t = setInterval(this.oneTick, 1000) // для дебага задержка = 1
        },
        pauseTimer(){
            this.isPlay = !this.isPlay;

            clearInterval(this.t);
        },
        stopTimer(){
            this.isPlay = true;
            this.pauseTimer();
            this.hour = 0;
            this.min = 0;
            this.sec = 0;
            this.time = "0"
        }
    }
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
        cursor: pointer;
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
        z-index: 1001;
    }
    .pause::after{
        content: '';
        position: absolute;
        width: 7px;
        height: 100%;
        top: 0;
        right: 0;
        background: white;
        z-index: 1001;
    }
    .pause::before{
        content: '';
        position: absolute;
        width: 7px;
        height: 100%;
        top: 0;
        left: 0;
        background: white;
        z-index: 1001;
    }
    .stop::before{
        content: '';
        position: absolute;
        width: 20px;
        height: 20px;
        top: 0;
        left: 0;
        background: white;
        z-index: 1001;
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
    .inactive .stop::before,
    .inactive .play::before{
        opacity: 0.5;
    }
</style>