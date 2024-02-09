<script>
export default {
  data() {
    return {
      companyDetails: {
        companyName: '',
        prospectiveCustomerEmail: '',
        fivetranContractEmail: '',
      },
      fivetranEngagementTimeline: {
        fivetranContractPeriod: 12,
        estimatedOnboardingTime: 4,
      },
      currentStaffingCosts: {
        averageSalary: 70000,
      }, 
      workSchedule: {
        hoursWorkedPerWeek: 40,
        weeksWorkedPerYear: 48,
      }
    }
  },
  computed: {
    equivalentHourlyRate() {
        return Math.floor((this.currentStaffingCosts.averageSalary) / (this.workSchedule.weeksWorkedPerYear * this.workSchedule.hoursWorkedPerWeek));
    }
  },
  methods: {
    kebabize(str) {
        return str.replace(/[A-Z]+(?![a-z])|[A-Z]/g, ($, ofs) => (ofs ? "-" : "") + $.toLowerCase())
    },
    sentencize(str) {
        let sentence = str.replace(/[A-Z]+(?![a-z])|[A-Z]/g, ($, ofs) => (ofs ? " " : "") + $.toLowerCase())
        return sentence.charAt(0).toUpperCase() + sentence.slice(1);
    },
  }
}
</script>

<template>
  <main>
    <h1>Fivetran ROI Calculator</h1>
    <section class="controls">
        <h2>Company profile</h2>
        <fieldset>
            <legend>Contact information</legend>
            <div class="input-label-vertical" v-for="(value, key) in this.companyDetails">
                <label :for="`${kebabize(key)}`">{{ sentencize(key) }}</label>
                <input type="text" v-model="companyDetails[key]" :id="`${kebabize(key)}`">
            </div>
        </fieldset>
        <fieldset>
            <legend>Fivetran engagement timeline</legend>
            <div class="input-row">
                <div class="input-label-box-horiz" v-for="(value, key, index) in this.fivetranEngagementTimeline">
                    <label :for="`${kebabize(key)}`">{{ sentencize(key) }}</label>
                    <input type="number" v-model="fivetranEngagementTimeline[key]" :defaultValue="value" :step="index === 0 ? 12 : 1">
                </div>
            </div>
        </fieldset>
        <fieldset>
            <legend>Current staffing costs</legend>
            <div class="input-row">
                <div class="input-label-box-horiz">
                    <label :for="`${kebabize('averageSalary')}`">{{ sentencize('averageSalary') }}</label>
                    <input type="number" v-model="currentStaffingCosts.averageSalary" :defaultValue="currentStaffingCosts.averageSalary" step="1000">
                </div>
                <div class="input-label-box-horiz">
                    <label :for="`${kebabize('equivalentHourlyRate')}`">{{ sentencize('equivalentHourlyRate') }}</label>
                    <output :for="`${kebabize('equivalentHourlyRate')}`" :value="equivalentHourlyRate"><span class="denom-dollar">{{ equivalentHourlyRate }}</span></output>
                </div>
            </div>
        </fieldset>
    </section>
  </main>
</template>

<style>

:root {
    --gray-05: #F7F8FA;
    --gray-10: #EDEFF2;
    --gray-40: #B0B2B8;
    --gray-90: #222222;
    --citron-10: #F4FFD3;
}

* {
    font-family: 'Inter', sans-serif;
}

/* resets */
fieldset {
    border: 0;
    padding: 0 0 0 0;
    margin: 0;
    min-width: 0;
    display: flex;
    flex-direction: column;
    gap: 16px;
}

body:not(:-moz-handler-blocked) fieldset {
    display: table-cell;
}

input { min-width: 0 }

main {
    width: 100%;
    display: flex;
    align-items: center;
    flex-direction: column;
}

h1, h2, h3, legend {
    display: block;
    font-weight: 600;
}

h1 {
    font-size: 36px;
    line-height: 48px;
}

h2 {
    font-size: 24px;
    line-height: 36px;
}

legend {
    font-size: 14px;
    line-height: 16px;
    border-bottom: 1px solid var(--gray-90);
    padding: 0px 0px 12px 0px;
    margin-bottom: 16px;
    width: 100%;
}

section {
    width: 100%;
    max-width: 1280px;
}

.controls {
    display: grid;
    grid-template-columns: repeat(12, 1fr);
    gap: 16px;
    padding: 40px;
    background: var(--gray-05);
    border-radius: 4px;
}

.controls:first-of-type fieldset:nth-of-type(1) {
    grid-column: 1 / span 4;
    grid-row: 2 / span 3;
}

.controls:first-of-type fieldset:nth-of-type(2) {
    grid-column: 6 / span 6;
}

.controls:first-of-type fieldset:nth-of-type(3) {
    grid-column: 6 / span 6;
}

.controls:first-of-type fieldset:nth-of-type(4) {
    grid-column: 6 / span 6;
}


input, output {
    padding: 6px 2px 6px 2px;
    font-size: 14px;
    line-height: 20px;
    border-radius: 2px;
}

input {
    border: 1px solid var(--gray-40);
}
    

.controls h2 {
    grid-column: 1 / span 12;
}

label {
    font-size: 14px;
    line-height: 20px;
    font-weight: 500;
}

.input-label-vertical {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.input-row {
    display: flex;
    gap: 20px;
    justify-content: stretch;
}

.input-label-box-horiz {
    display: flex;
    gap: 20px;
    flex: 1 1 50%;
    background: var(--gray-10);
    align-items: center;
    padding: 12px;
    border-radius: 4px;
    border: 1px solid var(--gray-40);
}

.input-label-box-horiz input, output {
    flex: 0 1 33.33%;
}

.input-label-box-horiz label {
    flex: 1 0 66.66%;
}

output {
    background: var(--citron-10)
}

.denom-dollar::before {
    content: '$'
}

</style>