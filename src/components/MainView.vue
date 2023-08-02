<template>
    <div class="w-full sm:px-[300px] px-6 mt-7 items-start flex flex-col justify-center">
        <div class="w-full flex flex-row items-center space-x-3 justify-end">
            <h3 class="text-black font-semibold text-xl">Date:</h3>
            <div>{{ currentDate }}</div>
        </div>

        <!-- NavLinks component -->
        <nav-links @show-section="showSection"></nav-links>

        <!-- Steps Walked Section -->
        <div>
            <div class="flex flex-col items-center mt-10">
                <div class="w-full">
                    <h2 class="text-2xl font-medium">Steps Walked</h2>
                </div>
                <input type="number" v-model="steps" class="mt-12 border-none outline-none" placeholder="Enter steps walked"
                    @input="calculateKilometers">
            </div>
            <hr class="w-full text-slate-300 mt-[45px] mb-4">
            <div>
                <p v-if="steps !== ''">You have walked {{ steps }} steps.</p>
            </div>
        </div>

        <!-- Ave Kilometer Section -->
        <div>
            <div class="flex flex-col items-center mt-14">
                <div class="w-full">
                    <h2 class="text-2xl font-medium">Average Kilometer Walked</h2>
                </div>
                <p v-if="kilometersWalkedPerHour !== null">
                    You have walked an average of {{ kilometersWalkedPerHour }} kilometers per hour.
                </p>
            </div>
            <hr class="w-full text-slate-300 mt-[45px] mb-4">
        </div>

        <!-- Calories Gone Section -->
        <div>
            <div class="flex flex-col items-center mt-10">
                <div class="w-full">
                    <h2 class="text-2xl font-medium">Calories Gone</h2>
                </div>
                <p v-if="caloriesBurnt !== null">
                    You have burnt approximately {{ caloriesBurnt.toFixed(2) }} calories.
                </p>
            </div>
            <hr class="w-full text-slate-300 mt-[45px] mb-4">
        </div>

        <!-- Blood Pressure Section -->
        <div>
            <div class="flex flex-col items-center mt-10 space-y-4">
                <div class="w-full">
                    <h2 class="text-2xl font-medium">Blood Pressure</h2>
                </div>

                <div v-if="!readingStarted">
                    <p v-if="!holdingDevice" class="italic text-gray-300">
                        Hold the device to start reading blood pressure...
                    </p>
                    <p v-else-if="holdingDuration < 10000">
                        Keep holding for {{ (10000 - holdingDuration) / 1000 }} seconds...
                    </p>
                    <p v-else>Reading Blood Pressure...</p>
                </div>

                <div v-else>
                    <h2>Your Blood Pressure:</h2>
                    <p>Systolic: {{ systolic }}</p>
                    <p>Diastolic: {{ diastolic }}</p>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script>
import NavLink from './NavLinks.vue'; // Import the NavLinks component

export default {
    components: {
        NavLink, // Register the NavLink component
    },
    data() {
        return {
            currentSection: '', // Set default value to an empty string
            readingStarted: false,
            holdingDevice: false,
            holdingDuration: 0,
            systolic: 0,
            diastolic: 0,
            bloodPressure: null,
            motionEventHandler: null,
            currentDate: '',
            steps: '',
            // Assuming a constant walking speed of 5 km/h (you can modify this value as needed)
            walkingSpeedKmPerHour: 5,
            kilometersWalkedPerHour: null,
            caloriesPerStep: 0.05, // Assuming a constant of 0.05 calories burned per step (you can modify this value)
            caloriesBurnt: null,
        };
    },
    mounted() {
        this.currentDate = this.getFormattedDate(new Date());
    },
    methods: {
        showSection(section) {
            this.currentSection = section;
        },
        getFormattedDate(date) {
            const options = {
                weekday: 'long',
                year: 'numeric',
                month: 'long',
                day: 'numeric',
            };
            return date.toLocaleDateString(undefined, options);
        },
        calculateKilometers() {
            if (!isNaN(this.steps) && this.steps >= 0) {
                // Calculate the average kilometers walked per hour based on the walking speed
                this.kilometersWalkedPerHour = this.steps / 1000 / this.walkingSpeedKmPerHour;
            } else {
                this.kilometersWalkedPerHour = null; // Reset the value if the input is invalid
            }
        },
        calculateCaloriesBurnt() {
            if (!isNaN(this.steps) && this.steps >= 0) {
                // Calculate calories burnt based on steps walked and calories per step
                this.caloriesBurnt = this.steps * this.caloriesPerStep;
            } else {
                this.caloriesBurnt = null; // Reset the value if the input is invalid
            }
        },
    },
};
</script>
  