<template>
    <!-- <div>
        <h1>Current Time</h1>
        <div class="time-widget">
            <div class="time-container">
                <div class="time-label">Current Time:</div>
                <div class="time-value">{{ currentTime }}</div>
            </div>
            <div class="time-decoration"></div>
        </div>
    </div>
    <hr> -->
    <div class="person">
        <h2>Calculate Left Day</h2>
        <p>{{ fullname }}</p>
        <p>Name: <input type="text" v-model="name"></p>  <!--v-model is used to bind the input field to the data property -->
        <p>Status: <input type="text" v-model="status"></p>  
        <p>ExemDay: <input type="date" value="2025-12-20" placeholder="yyyy-mm-dd"></p>
        <p><button @click="getAge">HOLD ON TIME</button></p>
        <!-- <span>Your age is: {{ age }}</span> -->
    </div>
    <hr>
    <div>
        <h2>You Have No Time:</h2>
        <div class="time-cards">
            <div class="time-card days">
                <span class="number">{{ timeObj.days || '0' }}</span>
                <span class="label">DAYS</span>
            </div>
            <div class="time-card">
                <span class="number">{{ timeObj.hours || '00' }}</span>
                <span class="label">HOURS</span>
            </div>
            <div class="time-card">
                <span class="number">{{ timeObj.minutes || '00' }}</span>
                <span class="label">MINUTES</span>
            </div>
            <div class="time-card">
                <span class="number">{{ timeObj.seconds || '00' }}</span>
                <span class="label">SECONDS</span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Person',
}
</script>

<script setup>
import { computed, ref } from 'vue';

let name = ref('卢子炯')
let status = ref('（考研版）')

const fullname = computed(() => {
    return `${name.value} ${status.value}`
})

const currentTime = ref(new Date().toLocaleTimeString())
setInterval(() => {
    currentTime.value = new Date().toLocaleTimeString()
}, 1000)

const age = ref(0)

const timeObj = ref({
    days: 0,
    hours: 0,
    minutes: 0,
    seconds: 0
})

function getAge() {
    const birthdayInput = document.querySelector('input[type="date"]').value
    if (!birthdayInput) {
        alert('Please enter your exem day')
        return
    }
    
    const birthday = new Date(birthdayInput)
    const calculateTimeDiff = () => {
        const today = new Date()
        const timeDiff = birthday.getTime() - today.getTime() + 8.5*60*60*1000;
        
        timeObj.value = {
        days: Math.floor(timeDiff / (1000 * 60 * 60 * 24)),
        hours: Math.floor((timeDiff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)),
        minutes: Math.floor((timeDiff % (1000 * 60 * 60)) / (1000 * 60)),
        seconds: Math.floor((timeDiff % (1000 * 60)) / 1000)
    };
    }
    
    calculateTimeDiff();
    const timer = setInterval(calculateTimeDiff, 1000);
    
    // Cleanup interval when component unmounts
    onUnmounted(() => {
        clearInterval(timer);
    });
}

</script>

<style scoped>
.person {
    max-width: 400px;
    margin: 30px auto;
    padding: 30px;
    border-radius: 12px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
    background: linear-gradient(to bottom right, #ffffff, #f8f9fa);
}

hr {
    border: none;
    height: 4px;
    /* background: linear-gradient(to right, #2128b0, #67e6bb); */
    margin: 25px auto;
    width: 80%;
    border-radius: 2px;
}

h2 {
    color: #2c3e50;
    margin-bottom: 25px;
    font-size: 24px;
    text-align: center;
    font-weight: 600;
}

.time-cards {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin: 20px auto;
    max-width: 800px;
}

.time-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
    background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
    background-size: 400% 400%;
    animation: gradient 15s ease infinite;
    border-radius: 15px;
    min-width: 120px;
    box-shadow: 0 10px 20px rgba(0,0,0,0.1);
}

.time-card.days {
    transform: scale(1.2);
    background: linear-gradient(-45deg, #FF416C, #FF4B2B);
    z-index: 1;
}

.time-card .number {
    font-size: 2.5em;
    font-weight: bold;
    color: white;
    text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
    margin-bottom: 5px;
}

.time-card .label {
    font-size: 0.9em;
    color: rgba(255,255,255,0.9);
    text-transform: uppercase;
    letter-spacing: 2px;
}

@keyframes gradient {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
}

/* 添加悬浮效果 */
.time-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 30px rgba(0,0,0,0.2);
    transition: all 0.3s ease;
}

.time-card.days:hover {
    transform: scale(1.25);
}

/* .countdown-display {
    animation: pulse 2s infinite ease-in-out;
    background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
    background-size: 400% 400%;
    animation: pulse 2s infinite ease-in-out, gradient 15s ease infinite;
    color: white;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    border-radius: 10px;
    padding: 20px;
    transition: all 0.3s ease;
}

@keyframes pulse {
    0% { transform: scale(1); }
    50% { transform: scale(1.02); }
    100% { transform: scale(1); }
}

@keyframes gradient {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
} */

p {
    margin: 15px 0;
}

input {
    width: 100%;
    padding: 10px;
    margin: 5px 0;
    border: 1px solid #ddd;
    border-radius: 6px;
    font-size: 14px;
    transition: border-color 0.3s ease;
}

input:focus {
    outline: none;
    border-color: #343cdb;
    box-shadow: 0 0 5px rgba(52, 169, 219, 0.3);
}

button {
    width: 100%;
    padding: 12px;
    background-color: #3498db;
    color: white;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 16px;
    font-weight: 500;
    transition: background-color 0.3s ease;
}

button:hover {
    background-color: #2980b9;
}

span {
    display: block;
    margin-top: 15px;
    text-align: center;
    color: #2c3e50;
    font-size: 16px;
    font-weight: 500;
}
.time-widget {
    background: linear-gradient(135deg, #2128b0, #67e6bb);
    border-radius: 15px;
    padding: 20px;
    margin: 20px auto;
    max-width: 450px;
    box-shadow: 0 10px 20px rgba(0,0,0,0.1);
}

.time-container {
    text-align: center;
}

.time-label {
    color: white;
    font-size: 1.2em;
    margin-bottom: 5px;
    text-transform: uppercase;
    letter-spacing: 2px;
}

.time-value {
    color: white;
    font-size: 2em;
    font-weight: bold;
    text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
}

.time-decoration {
    height: 3px;
    background: rgba(255,255,255,0.3);
    margin-top: 15px;
    border-radius: 2px;
}
</style>