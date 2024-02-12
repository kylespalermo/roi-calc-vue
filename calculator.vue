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
      },
      reportType: 'saas',
      dataStaffActivities: {
            saas: {
                buildingIntegrations: {
                    withoutFivetran: 5,
                    withoutFivetranLabel: 'Researching APIs, writing new code',
                    withFivetran: .5,
                    withFivetranLabel: 'Adding new connectors in Fivetran'
                }, 
                buildingTransformations: {
                    withoutFivetran: 10,
                    withoutFivetranLabel: 'Building transformations for new models',
                    withFivetran: 5,
                    withFivetranLabel: 'Building new models with Fivetran packages where possible',

                },
                maintainingIntegrations: {
                    withoutFivetran: 15,
                    withoutFivetranLabel: 'Updating API versions, adding new fields, fixing bugs',
                    withFivetran: 1,
                    withFivetranLabel: 'Monitoring Fivetran pipeline health'
                },
                maintainingTransformations: {
                    withoutFivetran: 5,
                    withoutFivetranLabel: 'Adding transformations for existing models',
                    withFivetran: 4,
                    withFivetranLabel: 'Fivetran managed packages - you just need to maintain custom code',
                },
                deploymentAndOrchestration: {
                    withoutFivetran: 5,
                    withoutFivetranLabel: 'Promoting changes through dev/test, Co-ordinating pipeline runs',
                    withFivetran: 1,
                    withFivetranLabel: 'Fivetran API, scheduler, transformations'
                }
            },
            databases: {
                totalBuildTimePerEngineer: {
                    withoutFivetran: 5,
                    withoutFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',
                    withFivetran: 5,
                    withFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',
                },
                maintenanceTimePerEngineer: {
                    withoutFivetran: 5,
                    withoutFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',
                    withFivetran: 5,
                    withFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',
                },
                dataUptime: {
                    withoutFivetran: 99.90,
                    withoutFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',
                    withFivetran: 99.99,
                    withFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',
                },
                costOfDestination: {
                    withoutFivetran: 100000,
                    withoutFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',
                    withFivetran: 100000,
                    withFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',
                }
            }
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
    <section class="controls" id="company-profile">
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
        <fieldset>
            <legend>Work schedule</legend>
            <div class="input-row">
                <div class="input-label-box-horiz">
                    <label :for="`${kebabize('hoursWorkedPerWeek')}`">{{ sentencize('hoursWorkedPerWeek') }}</label>
                    <input type="number" v-model="workSchedule.hoursWorkedPerWeek" :defaultValue="workSchedule.hoursWorkedPerWeek">
                </div>
                <div class="input-label-box-horiz">
                    <label :for="`${kebabize('weeksWorkedPerYear')}`">{{ sentencize('weeksWorkedPerYear') }}</label>
                    <input type="number" v-model="workSchedule.weeksWorkedPerYear" :defaultValue="workSchedule.weeksWorkedPerYear">
                </div>
            </div>
        </fieldset>
    </section>
    <section class="controls" id="data-staff-activities">
        <h2>Data staff activities</h2>
        <fieldset class="segmented-control" id="report-type-control">
            <div>Select a report type:</div>
            <div>
                <input type="radio" id="saas" name="report-type" value="saas" v-model="reportType" checked />
                <label for="saas">SaaS</label>
            </div>
            <div>
                <input type="radio" id="databases" name="report-type" value="databases" v-model="reportType" />
                <label for="databases">Databases</label>
            </div>
        </fieldset>
        <div id="engineering-function">
            <div class="table-header">
                <span class="input-table-header">Engineering function</span>
                <span class="input-table-header">Activities without Fivetran</span>
                <span class="input-table-header">Activities with Fivetran</span>
            </div>
            <fieldset class="data-staff-function" v-for="(value, key) in this.dataStaffActivities[this.reportType]">
                <div>{{ sentencize(key) }}</div>
                <div class="input-label-caption">
                    <label :for="`${kebabize(key)}`"><i>{{ value.withoutFivetranLabel }}</i></label>
                    {{ console.log(value) }}
                    <input type="number" v-model="value.withoutFivetran" :defaultValue="value.withoutFivetran">
                </div>
                <div class="input-label-caption">
                    <label :for="`${kebabize(key)}`"><i>{{ value.withFivetranLabel }}</i></label>
                    {{ console.log(value) }}
                    <input type="number" v-model="value.withFivetran" :defaultValue="value.withFivetran">
                </div>
            </fieldset>
        </div>
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
    gap: 60px;
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
    display: flex;
    flex-direction: column;
}

.controls:first-of-type fieldset:nth-of-type(2) {
    grid-column: 6 / span 6;
    margin-bottom: 32px;
}

.controls:first-of-type fieldset:nth-of-type(3) {
    grid-column: 6 / span 6;
    margin-bottom: 32px;
}

.controls:first-of-type fieldset:nth-of-type(4) {
    grid-column: 6 / span 6;
    margin-bottom: 32px;
}


input, output {
    padding: 6px 2px 6px 12px;
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

label, .input-table-header {
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
    flex: 0 1 40%;
}

.input-label-box-horiz label {
    flex: 1 0 60%;
}

output {
    background: var(--citron-10)
}

.denom-dollar::before {
    content: '$'
}

#report-type-control {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    grid-column: 1 / span 12;
    margin-bottom: 48px;
}

#engineering-function {
    grid-column: 1 / span 9;
    display: flex;
    flex-direction: column;
    gap: 20px;
    legend {
        padding: 0px;
        border: none;
    }
    .table-header {
        display: grid;
        grid-template-columns: repeat(9, 1fr);
        gap: 20px;
        span {
            grid-column: auto / span 3;
            text-align: right;
        }
        span:nth-child(1) {
            text-align: left;
        }
    }

}

.table-header {
    padding-bottom: 12px;
    border-bottom: 1px solid var(--gray-90);
}

.data-staff-function {
    display: grid;
    grid-template-columns: repeat(9, 1fr);
    gap: 20px;
    * {
        grid-column: auto / span 3;
    }
}

.input-label-caption {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 12px;
    label {
        font-size: 13px;
        line-height: 16px;
        font-weight: 400;
        text-align: right;
        flex: 0 0 60%;
    }
}

</style>