<template>
    <div class="sm:px-[300px] px-6 w-full flex mt-10 flex-row items-center justify-start space-x-3">
        <!-- Nav buttons (visible on larger screens) -->
        <button class="hidden sm:block bg-gradient-to-r from-slate-600 to bg-green-600 px-3 py-1 text-white rounded"
            @click="showSection('StepsWalked')">
            Steps Walked
        </button>
        <button class="hidden sm:block bg-gradient-to-r from-slate-600 to bg-green-600 px-3 py-1 text-white rounded"
            @click="showSection('AveKilometer')">
            Ave Kilometer
        </button>
        <button class="hidden sm:block bg-gradient-to-r from-slate-600 to bg-green-600 px-3 py-1 text-white rounded"
            @click="showSection('CaloriesGone')">
            Calories gone
        </button>
        <button class="hidden sm:block bg-gradient-to-r from-slate-600 to bg-green-600 px-3 py-1 text-white rounded"
            @click="showSection('BloodPressure')">
            Blood Pressure
        </button>

        <!-- Hamburger button (visible on smaller screens) -->
        <button class="sm:hidden bg-gradient-to-r from-slate-600 to bg-green-600 px-3 py-1 text-white rounded"
            @click="toggleLinks">
            <i :class="{
                'fa-solid fa-chevron-left': showLinks,
                'fa-solid fa-chevron-right': !showLinks,
            }"></i>
        </button>

        <!-- Links (visible on smaller screens) -->
        <div class="sm:hidden space-y-2" v-if="showLinks">
            <button class="block bg-gradient-to-r from-slate-600 to bg-green-600 px-3 py-1 text-white rounded"
                @click="showSection('StepsWalked')">
                Steps Walked
            </button>
            <button class="block bg-gradient-to-r from-slate-600 to bg-green-600 px-3 py-1 text-white rounded"
                @click="showSection('AveKilometer')">
                Ave Kilometer
            </button>
            <button class="block bg-gradient-to-r from-slate-600 to bg-green-600 px-3 py-1 text-white rounded"
                @click="showSection('CaloriesGone')">
                Calories gone
            </button>
            <button class="block bg-gradient-to-r from-slate-600 to bg-green-600 px-3 py-1 text-white rounded"
                @click="showSection('BloodPressure')">
                Blood Pressure
            </button>
        </div>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            showLinks: false,
        };
    },
    methods: {
        toggleLinks() {
            this.showLinks = !this.showLinks;
        },
        showSection(section) {
            this.$emit('show-section', section);
        },
    },
};
</script>
  