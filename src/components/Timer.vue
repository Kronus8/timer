<template>
    <div class="flex justify-center items-center h-screen">
        <div class="card w-96 bg-base-200 shadow-xl">
            <div class="card-body">
                <h1 class="card-title justify-center text-2xl">Timer</h1>
                <div class="flex justify-center items-center">
                    <span class="countdown font-mono text-3xl">
                        <span :style="{ '--value': hours }"></span>:
                        <span :style="{ '--value': mins }"></span>:
                        <span :style="{ '--value': seconds }"></span>
                    </span>
                </div>
                <div class="card-actions justify-center">
                    <button class="btn btn-primary" @click="startTimer">Start</button>
                    <button class="btn btn-error btn-outline" @click="stopTimer">Stop</button>
                    <button class="btn btn-accent btn-outline" @click="resetTimer">Reset</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
    import { ref } from 'vue';

    const hours = ref(0);
    const mins = ref(0);
    const seconds = ref(0);
    const stopTime = ref(true);
    const intervalID = ref(0);

    function startTimer() {
        if (stopTime.value == true) {
            stopTime.value = false;
            intervalID.value = setInterval(timerHandler, 1000);
        }
    }

    function stopTimer () {
        if (stopTime.value == false) {
            stopTime.value = true;
            clearInterval(intervalID.value);
        }
    }

    function resetTimer() {
        //hours.value = 0; 
        //mins.value = 0; 
        //seconds.value = 0;
        stopTimer();
        hours.value = mins.value = seconds.value = 0;
    }

    function timerHandler() {
        if (stopTime.value == false) {
            seconds.value = seconds.value + 1;

            if (seconds.value == 60) {
                mins.value = mins.value + 1;
                seconds.value = 0;
            }

            if (mins.value == 60) {
                hours.value = hours.value + 1;
                mins.value = 0;
                seconds.value = 0;
            }
        }
    }
</script>