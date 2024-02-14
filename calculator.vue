<script>
//default value appears to be unecessary when using v-model
export default {
    data() {
        return {
            complete: true,
            companyDetails: {
                companyName: '',
                prospectiveCustomerEmail: '',
                fivetranContactEmail: '',
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
            numberOfEngineersWorkingOnPipelines: null,
            dataStackAndStaffing: {
                saas: {
                    engineeringFunction: {
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
                    additionalComparisons: {
                        annualCostsOfPipelineRelatedInfrastructure: {
                            withoutFivetran: null,
                            withFivetran: null,
                        }
                    }
                },
                databases: {
                    engineeringFunction: {
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
                    },
                    additionalComparisons: {
                        annualCostsOfPipelineRelatedInfrastructure: {
                            withoutFivetran: null,
                            withFivetran: null,
                        },
                        dataUptime: {
                            withoutFivetran: null,
                            withFivetran: 99.99
                        },
                        costOfDestination: {
                            withoutFivetran: null,
                            withFivetran: null,
                        }
                    },
                    additionalCostInputs: {
                        costOfDataDowntime: null,
                        costOfAlternative: null,
                    }
                }
            },
            outputs: {
                companyDetails: {
                companyName: '',
                prospectiveCustomerEmail: '',
                fivetranContractEmail: '',
                },
            },
        }
    },
    computed: {
        equivalentHourlyRate() {
            return Math.floor((this.currentStaffingCosts.averageSalary) / (this.workSchedule.weeksWorkedPerYear * this.workSchedule.hoursWorkedPerWeek));
        },
        calculateBuildMaintainCosts() {
            
            let calcs = {
                annualCostOfBuildingPipelines: {
                    currentCosts: '',
                    costsWithFivetran: '',
                },
                annualCostOfMaintainingPipelines: {
                    currentCosts: '',
                    costsWithFivetran: '',
                },
            }

            calcs.annualCostOfBuildingPipelines.currentCosts = this.calculateAnnualCosts(this.dataStackAndStaffing[this.reportType].engineeringFunction.buildingIntegrations.withoutFivetran, this.dataStackAndStaffing[this.reportType].engineeringFunction.buildingTransformations.withoutFivetran)
            calcs.annualCostOfBuildingPipelines.costsWithFivetran = this.calculateAnnualCosts(this.dataStackAndStaffing[this.reportType].engineeringFunction.buildingIntegrations.withFivetran, this.dataStackAndStaffing[this.reportType].engineeringFunction.buildingTransformations.withFivetran)

            calcs.annualCostOfMaintainingPipelines.currentCosts = this.calculateAnnualCosts(this.dataStackAndStaffing[this.reportType].engineeringFunction.maintainingIntegrations.withoutFivetran, this.dataStackAndStaffing[this.reportType].engineeringFunction.maintainingTransformations.withoutFivetran, this.dataStackAndStaffing[this.reportType].engineeringFunction.deploymentAndOrchestration.withoutFivetran)
            calcs.annualCostOfMaintainingPipelines.costsWithFivetran = this.calculateAnnualCosts(this.dataStackAndStaffing[this.reportType].engineeringFunction.maintainingIntegrations.withFivetran, this.dataStackAndStaffing[this.reportType].engineeringFunction.maintainingTransformations.withFivetran, this.dataStackAndStaffing[this.reportType].engineeringFunction.deploymentAndOrchestration.withFivetran)
            
     

            return calcs;
        },
        totalWeeklyMaintainanceTimeWithFivetran() {
            let hrs = 0
            for (let category in this.dataStackAndStaffing[this.reportType].engineeringFunction) {
                hrs += this.dataStackAndStaffing[this.reportType].engineeringFunction[category].withFivetran;
            }
            return hrs;
        },
        totalWeeklyMaintainanceTimeWithoutFivetran() {
            let hrs = 0
            for (let category in this.dataStackAndStaffing[this.reportType].engineeringFunction) {
                hrs += this.dataStackAndStaffing[this.reportType].engineeringFunction[category].withoutFivetran;
            }
            return hrs;
        }
    },
    methods: {
        formatDollars(num) {
            const numOptions = { style: 'currency', currency: 'USD' };
            const numberFormat = new Intl.NumberFormat('en-US', numOptions);

            return numberFormat.format(num)
        },
        calculateAnnualCosts(...tasks){

            const numOptions = { style: 'currency', currency: 'USD' };
            const numberFormat = new Intl.NumberFormat('en-US', numOptions);

            let taskHours = 0;
            tasks.forEach(task => {
                taskHours += task;
            })
            return taskHours * this.workSchedule.weeksWorkedPerYear * this.equivalentHourlyRate * this.numberOfEngineersWorkingOnPipelines;
        },
        kebabize(str) {
            return str.replace(/[A-Z]+(?![a-z])|[A-Z]/g, ($, ofs) => (ofs ? "-" : "") + $.toLowerCase())
        },
        sentencize(str) {
            let sentence = str.replace(/[A-Z]+(?![a-z])|[A-Z]/g, ($, ofs) => (ofs ? " " : "") + $.toLowerCase())
            return sentence.charAt(0).toUpperCase() + sentence.slice(1);
        },
        submitForm() {
            var reqs = document.querySelectorAll("[required]")
            var numInvalid = 0;
            reqs.forEach(req => {
                if (!req.value) {
                    req.classList.add("invalid")
                    numInvalid++;
                } else {
                    req.classList.remove("invalid")
                }
            })
            if (numInvalid === 0) {
                this.complete = true;
                this.updateOutputs();
            }
        },
        updateOutputs(){
            this.outputs.companyDetails.companyName = this.companyDetails.companyName;
            this.outputs.companyDetails.prospectiveCustomerEmail = this.companyDetails.prospectiveCustomerEmail;
            this.outputs.companyDetails.fivetranContactEmail = this.companyDetails.fivetranContactEmail;
        }
    },
}
</script>

<template>
    <main>
        <form onsubmit="return false">
            <h1>Fivetran ROI Calculator</h1>
            <div class="form-block controls" id="company-profile">
                <h2>Company profile</h2>
                <fieldset>
                    <legend>Contact information</legend>
                    <div class="input-label-vertical" v-for="(value, key) in this.companyDetails">
                        <label :for="`${kebabize(key)}`">{{ sentencize(key) }}</label>
                        <input type="text" v-model="companyDetails[key]" :id="`${kebabize(key)}`" required>
                    </div>
                </fieldset>
                <fieldset>
                    <legend>Fivetran engagement timeline</legend>
                    <div class="input-row">
                        <div class="input-label-box-horiz" v-for="(value, key, index) in this.fivetranEngagementTimeline">
                            <label :for="`${kebabize(key)}`">{{ sentencize(key) }}</label>
                            <input type="number" v-model="fivetranEngagementTimeline[key]" :defaultValue="value"
                                :step="index === 0 ? 12 : 1">
                        </div>
                    </div>
                </fieldset>
                <fieldset>
                    <legend>Current staffing costs</legend>
                    <div class="input-row">
                        <div class="input-label-box-horiz">
                            <label :for="`${kebabize('averageSalary')}`">{{ sentencize('averageSalary') }}</label>
                            <input type="number" v-model="currentStaffingCosts.averageSalary"
                                :defaultValue="currentStaffingCosts.averageSalary" step="1000">
                        </div>
                        <div class="input-label-box-horiz">
                            <label :for="`${kebabize('equivalentHourlyRate')}`">{{ sentencize('equivalentHourlyRate')
                            }}</label>
                            <output :for="`${kebabize('equivalentHourlyRate')}`" :value="equivalentHourlyRate"><span
                                    class="denom-dollar">{{ equivalentHourlyRate }}</span></output>
                        </div>
                    </div>
                </fieldset>
                <fieldset>
                    <legend>Work schedule</legend>
                    <div class="input-row">
                        <div class="input-label-box-horiz">
                            <label :for="`${kebabize('hoursWorkedPerWeek')}`">{{ sentencize('hoursWorkedPerWeek') }}</label>
                            <input type="number" v-model="workSchedule.hoursWorkedPerWeek"
                                :defaultValue="workSchedule.hoursWorkedPerWeek">
                        </div>
                        <div class="input-label-box-horiz">
                            <label :for="`${kebabize('weeksWorkedPerYear')}`">{{ sentencize('weeksWorkedPerYear') }}</label>
                            <input type="number" v-model="workSchedule.weeksWorkedPerYear"
                                :defaultValue="workSchedule.weeksWorkedPerYear">
                        </div>
                    </div>
                </fieldset>
            </div>
            <div class="form-block controls" id="data-staff-activities">
                <h2>Data staff activities</h2>
                <div class="input-label-box-horiz">
                    <label for="number-of-engineers-working-on-pipelines">Number of engineers working on pipelines</label>
                    <input type="number" v-model="numberOfEngineersWorkingOnPipelines" required>
                </div>
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
                    <div class="table-header three-column">
                        <span class="input-table-header text-left">Engineering function</span>
                        <span class="input-table-header text-right">Activities without Fivetran</span>
                        <span class="input-table-header text-right">Activities with Fivetran</span>
                    </div>
                    <fieldset class="data-staff-function" v-for="(value, key) in this.dataStackAndStaffing[this.reportType].engineeringFunction">
                        <div>{{ sentencize(key) }}</div>
                        <div class="input-label-caption">
                            <label :for="`${kebabize(key)}`"><i>{{ value.withoutFivetranLabel }}</i></label>
                            <input type="number" :for="`${kebabize(key)}`" :id="`${kebabize(key)}`"
                                v-model="value.withoutFivetran" :defaultValue="value.withoutFivetran">
                        </div>
                        <div class="input-label-caption">
                            <label :for="`${kebabize(key)}`"><i>{{ value.withFivetranLabel }}</i></label>
                            <input type="number" v-model="value.withFivetran" :defaultValue="value.withFivetran">
                        </div>
                    </fieldset>
                    <div v-if="this.reportType === 'saas'" class="data-staff-function-outputs">
                        <div>Total weekly pipeline maintenance time per engineer</div>
                        <div class="output-wrapper"><output><span class="denom-hours">{{ totalWeeklyMaintainanceTimeWithoutFivetran }}</span></output></div>
                        <div class="output-wrapper"><output><span class="denom-hours">{{ totalWeeklyMaintainanceTimeWithFivetran }}</span></output></div>
                    </div>
                </div>
                <fieldset class="additional-database-inputs" v-if="this.reportType === 'databases'">
                    <legend>Additional database inputs</legend>
                    <div class="input-row">
                        <div class="input-label-box-horiz">
                            <label for="cost-of-data-downtime-per-hour">Cost of data downtime per hour</label>
                            <input type="number" id="cost-of-data-downtime-per-hour" name="cost-of-data-downtime-per-hour" v-model="dataStackAndStaffing.databases.additionalCostInputs.costOfDataDowntime">
                        </div>
                        <div class="input-label-box-horiz">
                            <label for="cost-of-alternative">Cost of alternative</label>
                            <input type="number" id="cost-of-data-alternative" name="cost-of-alternative" v-model="dataStackAndStaffing.databases.additionalCostInputs.costOfAlternative">
                        </div>
                    </div>
                </fieldset>
            </div>
            <input type="submit" value="Generate report" id="generate-report" @click="submitForm">
        </form>
        <div class="form-block report" v-if="complete">
            <div class="heading-block">
                <hgroup>
                    <h2>{{ outputs.companyDetails.companyName }}</h2>
                    <p> Fivetran SaaS Connectors - ROI Analysis</p>
                    <p>Generated {{ new Date().toLocaleDateString("en-US") }}</p>
                    <p>Questions? Contact {{ outputs.companyDetails.fivetranContactEmail }}</p>
                </hgroup>
                <div>
                    <img src="fivetran.svg">
                    <span>fivetran.com</span>
                </div>
            </div>
            <div class="table-header four-column">
                <span class="input-table-header text-left">Activities to build & maintain pipelines</span>
                <span class="input-table-header text-center">Current costs</span>
                <span class="input-table-header text-center">Costs w/Fivetran</span>
                <span class="input-table-header text-center">Fivetran cost savings<span class="annotation"><br>(Current costs less costs w/Fivetran)</span></span>
            </div>
            <div class="table-row four-column">
                <span class="input-table-header text-left">Annual cost of building pipelines</span>
                <span class="input-table-header text-center">{{ this.formatDollars(this.calculateBuildMaintainCosts.annualCostOfBuildingPipelines.currentCosts) }}</span>
                <span class="input-table-header text-center">{{ this.formatDollars(this.calculateBuildMaintainCosts.annualCostOfBuildingPipelines.costsWithFivetran) }}</span>
                <span class="input-table-header text-center">{{ this.formatDollars(this.calculateBuildMaintainCosts.annualCostOfBuildingPipelines.currentCosts - this.calculateBuildMaintainCosts.annualCostOfBuildingPipelines.costsWithFivetran) }}</span>
            </div>
            <div class="table-row four-column">
                <span class="input-table-header text-left">Annual cost of maintaining pipelines</span>
                <span class="input-table-header text-center">{{ this.formatDollars(this.calculateBuildMaintainCosts.annualCostOfMaintainingPipelines.currentCosts) }}</span>
                <span class="input-table-header text-center">{{ this.formatDollars(this.calculateBuildMaintainCosts.annualCostOfMaintainingPipelines.costsWithFivetran) }}</span>
                <span class="input-table-header text-center">{{ this.formatDollars(this.calculateBuildMaintainCosts.annualCostOfMaintainingPipelines.currentCosts - this.calculateBuildMaintainCosts.annualCostOfMaintainingPipelines.costsWithFivetran) }}</span>
            </div>
            <div class="table-row four-column">
                <span class="input-table-header text-left">Annual cost of pipeline related infrastructure</span>
                <span class="input-table-header text-center">{{ this.formatDollars(this.calculateBuildMaintainCosts.annualCostOfMaintainingPipelines.currentCosts) }}</span>
                <span class="input-table-header text-center">{{ this.formatDollars(this.calculateBuildMaintainCosts.annualCostOfMaintainingPipelines.costsWithFivetran) }}</span>
                <span class="input-table-header text-center">{{ this.formatDollars(this.calculateBuildMaintainCosts.annualCostOfMaintainingPipelines.currentCosts - this.calculateBuildMaintainCosts.annualCostOfMaintainingPipelines.costsWithFivetran) }}</span>
            </div>
        </div>
    </main>
</template>

<style>
:root {
    --gray-05: #F7F8FA;
    --gray-10: #EDEFF2;
    --gray-40: #B0B2B8;
    --gray-90: #222222;
    --citron-10: #F4FFD3;
    --blue-60: #306bea;
}

* {
    font-family: 'Inter', sans-serif;
    box-sizing: border-box;
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

input {
    min-width: 0
}

form {
    width: 100%;
    display: flex;
    align-items: center;
    flex-direction: column;
    gap: 60px;
}

h1,
h2,
h3,
legend,
.input-table-header {
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

.form-block,
.report {
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


input,
output {
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

.input-label-box-horiz input,
output {
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
    grid-column: 1 / span 10;
    display: flex;
    flex-direction: column;
    gap: 20px;

    legend {
        padding: 0px;
        border: none;
    }
}

.four-column {
    grid-template-columns: repeat(4, 1fr);
}

.three-column {
    grid-template-columns: repeat(3, 1fr);
}

.table-header, .table-row {
    padding-bottom: 12px;
    border-bottom: 1px solid;
    display: grid;
    align-items: center;
    gap: 20px;
}

.table-header {
    border-color: var(--gray-90);
}

.table-row {
    border-color: var(--gray-40);
}


.data-staff-function,
.data-staff-function-outputs {
    display: grid;
    grid-template-columns: repeat(9, 1fr);
    gap: 20px;

    * {
        grid-column: auto / span 3;
    }

    .output-wrapper {
        display: flex;
        align-items: center;
        justify-content: flex-end;

        output {
            flex: 0 1 32%;
        }
    }
}

.data-staff-function-outputs {
    padding-top: 12px;
    border-top: 1px solid var(--gray-90)
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

.denom-hours:after {
    content: ' hrs'
}

.additional-database-inputs {
    grid-column: 1 / span 8;
    margin-top: 36px;
}

input[type=submit] {
    background: var(--blue-60);
    color: white;
    border: none;
    padding: 8px 16px 8px 16px;
    border-radius: 4px;
    font-size: 16px;
    line-height: 20px;
    font-weight: 500;
    cursor: pointer;
}

.report {
    display: grid;
    border: 1px solid var(--gray-90);
    gap: 60px;
    padding: 60px;

    img {
        grid-column: 2 / span 1;
        grid-row: 1 / span 1;
        justify-self: end;
    }
}

main {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.heading-block {
    display: flex;
    justify-content: space-between;
    hgroup, div {
        display: flex;
        flex-direction: column;
        gap: 6px;
        * {
            margin: 0;
            padding: 0;
        }
    }
}

.invalid,
.invalid:focus {
    outline: red;
    border-color: red;
}

.text-center {
    text-align: center;
}

.text-left {
    text-align: left;
}

.text-right {
    text-align: right;
}


.annotation {
    font-size: 12px;
    line-height: 16px;
    font-weight: 400;
}

</style>