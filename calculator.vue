<script>
//default value appears to be unecessary when using v-model
export default {
    data() {
        return {
            complete: false, //toggle this to true to keep report visible for dev purposes
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
                            withoutFivetranLabel: 'Promoting changes through dev/test, Co-ordinating pipeline runs',
                            withFivetran: null,
                            withFivetranLabel: 'Fivetran API, scheduler, transformations'
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
                        }
                    },
                    additionalComparisons: {
                        annualCostsOfPipelineRelatedInfrastructure: {
                            withoutFivetran: null,
                            withoutFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',
                            withFivetran: null,
                            withFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',

                        },
                        dataUptime: {
                            withoutFivetran: null,//input an industry average here
                            withoutFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',
                            withFivetran: 99.99,
                            withFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',
                        },
                        costOfDestination: {
                            withoutFivetran: null,//need to input a default here?
                            withoutFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',
                            withFivetran: null,//need to input a default here?
                            withFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',
                        }
                    },
                    additionalCostInputs: {
                        costOfDataDowntime: null,//need to input a default here?
                        costOfAlternative: null,//need to input a default here?
                    }
                }
            },
            reportOutputs: {
                companyDetails: {
                    companyName: '',
                    prospectiveCustomerEmail: '',
                    fivetranContractEmail: '',
                },
                activitiesToBuildAndMaintainPipelines: {
                    annualCostOfBuildingPipelines: {
                        currentCosts: '',
                        costsWithFivetran: '',
                        fivetranCostSavings: ''
                    },
                    annualCostOfMaintainingPipelines: {
                        currentCosts: '',
                        costsWithFivetran: '',
                        fivetranCostSavings: ''
                    },
                    annualCostsOfPipelineRelatedInfrastructure: {
                        currentCosts: '',
                        costsWithFivetran: '',
                        fivetranCostSavings: ''
                    }
                },
                costOfEnvironment: {
                    currentCosts: '',
                    costsWithFivetran: '',
                    fivetranCostSavings: ''
                },
                costOfFivetran: {
                    currentCosts: null,
                    costsWithFivetran: '',
                    fivetranCostSavings: ''
                },
                finalSavingsAnalysis: {
                    currentCosts: '',
                    costsWithFivetran: '',
                    fivetranCostSavings: ''
                }
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

            let engFuncs = this.dataStackAndStaffing[this.reportType].engineeringFunction

            if (this.reportType == "saas") {
                //can wrap this in an if statement and provide alternative calculations for databases. The keys are different for dbs.
                calcs.annualCostOfBuildingPipelines.currentCosts = this.calculateAnnualCosts(engFuncs.buildingIntegrations.withoutFivetran, engFuncs.buildingTransformations.withoutFivetran)
                calcs.annualCostOfBuildingPipelines.costsWithFivetran = this.calculateAnnualCosts(engFuncs.buildingIntegrations.withFivetran, engFuncs.buildingTransformations.withFivetran)

                calcs.annualCostOfMaintainingPipelines.currentCosts = this.calculateAnnualCosts(engFuncs.maintainingIntegrations.withoutFivetran, engFuncs.maintainingTransformations.withoutFivetran, engFuncs.deploymentAndOrchestration.withoutFivetran)
                calcs.annualCostOfMaintainingPipelines.costsWithFivetran = this.calculateAnnualCosts(engFuncs.maintainingIntegrations.withFivetran, engFuncs.maintainingTransformations.withFivetran, engFuncs.deploymentAndOrchestration.withFivetran)
            } else if (this.reportType == "databases") {
                calcs.annualCostOfBuildingPipelines.currentCosts = this.calculateAnnualCosts(engFuncs.totalBuildTimePerEngineer.withoutFivetran)
                calcs.annualCostOfBuildingPipelines.costsWithFivetran = this.calculateAnnualCosts(engFuncs.totalBuildTimePerEngineer.withFivetran)

                calcs.annualCostOfMaintainingPipelines.currentCosts = this.calculateAnnualCosts(engFuncs.maintenanceTimePerEngineer.withoutFivetran)
                calcs.annualCostOfMaintainingPipelines.costsWithFivetran = this.calculateAnnualCosts(engFuncs.maintenanceTimePerEngineer.withFivetran)
            }

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
        // async getJSON() {
        //     //create method called send to s3 or whatever, and another called email to marketo. For s3, just a fetch to the endpoint, which Jason can give me. Saves the file and returns whatver data I need. Generate unique Id method. Just posting the json to the endpoint, with the ID we generated. {id}.json
        //     let endpoint = "https://s3.amazonaws.com/go.fivetran.com/roi-calculator/results/kyle-test.json"
        //     const results = await fetch(endpoint)
        //     const response = await results.json()
        //     console.log(response)
        // },
        calculateAnnualCosts(...tasks) {

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
                this.updatereportOutputs();
            }
        },
        updatereportOutputs() {
            //passes data from reactive slots and computed properties into a report object
            //this allows us to cache the data that populates the report, so the report isn't reactive if the inputs are adjsuted after generating it
            //the report only updates after this function runs

            //shorten the reference to report output object to make them more readable
            let r = this.reportOutputs;

            //update companyDetails 
            r.companyDetails.companyName = this.companyDetails.companyName;
            r.companyDetails.prospectiveCustomerEmail = this.companyDetails.prospectiveCustomerEmail;
            r.companyDetails.fivetranContactEmail = this.companyDetails.fivetranContactEmail;

            //update activities to build and maintain pipelines
            //annual cost of building pipelines
            r.activitiesToBuildAndMaintainPipelines.annualCostOfBuildingPipelines.currentCosts = this.formatDollars(this.calculateBuildMaintainCosts.annualCostOfBuildingPipelines.currentCosts);
            r.activitiesToBuildAndMaintainPipelines.annualCostOfBuildingPipelines.costsWithFivetran = this.formatDollars(this.calculateBuildMaintainCosts.annualCostOfBuildingPipelines.costsWithFivetran);
            r.activitiesToBuildAndMaintainPipelines.annualCostOfBuildingPipelines.fivetranCostSavings = this.formatDollars(this.calculateBuildMaintainCosts.annualCostOfBuildingPipelines.currentCosts - this.calculateBuildMaintainCosts.annualCostOfBuildingPipelines.costsWithFivetran);

            //update annuual cost of maintaining pipelines
            r.activitiesToBuildAndMaintainPipelines.annualCostOfMaintainingPipelines.currentCosts = this.formatDollars(this.calculateBuildMaintainCosts.annualCostOfMaintainingPipelines.currentCosts)
            r.activitiesToBuildAndMaintainPipelines.annualCostOfMaintainingPipelines.costsWithFivetran = this.formatDollars(this.calculateBuildMaintainCosts.annualCostOfMaintainingPipelines.costsWithFivetran)
            r.activitiesToBuildAndMaintainPipelines.annualCostOfMaintainingPipelines.fivetranCostSavings = this.formatDollars(this.calculateBuildMaintainCosts.annualCostOfMaintainingPipelines.currentCosts - this.calculateBuildMaintainCosts.annualCostOfMaintainingPipelines.costsWithFivetran)


            r.activitiesToBuildAndMaintainPipelines.annualCostsOfPipelineRelatedInfrastructure.currentCosts = this.formatDollars(this.dataStackAndStaffing[this.reportType].additionalComparisons.annualCostsOfPipelineRelatedInfrastructure.withFivetran)
            r.activitiesToBuildAndMaintainPipelines.annualCostsOfPipelineRelatedInfrastructure.costsWithFivetran = this.formatDollars(this.dataStackAndStaffing[this.reportType].additionalComparisons.annualCostsOfPipelineRelatedInfrastructure.withoutFivetran);
            r.activitiesToBuildAndMaintainPipelines.annualCostsOfPipelineRelatedInfrastructure.fivetranCostSavings = this.formatDollars(this.dataStackAndStaffing[this.reportType].additionalComparisons.annualCostsOfPipelineRelatedInfrastructure.withFivetran - this.dataStackAndStaffing[this.reportType].additionalComparisons.annualCostsOfPipelineRelatedInfrastructure.withoutFivetran);

            // this.reportOutputs.costOfEnvironment.currentCosts
            // this.reportOutputs.costOfEnvironment.costsWithFivetran
            // this.reportOutputs.costOfEnvironment.fivetranCostSavings
            // this.reportOutputs.costOfFivetran.costsWithFivetran
            // this.reportOutputs.finalSavingsAnalysis.currentCosts
            // this.reportOutputs.finalSavingsAnalysis.costsWithFivetran
            // this.reportOutputs.finalSavingsAnalysis.fivetranCostSavings
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
                <!-- Beging data stack and staffing section -->
                <h2>Data stack and staffing</h2>
                <div class="input-label-box-horiz grid-child-span-3">
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
                <!-- Engineering function rows, render for both saas and databases -->
                <div class="data-stack-staffing-field-group">
                    <div class="table-header three-column">
                        <span class="input-table-header text-left">Engineering function</span>
                        <span class="input-table-header text-right">Activities without Fivetran</span>
                        <span class="input-table-header text-right">Activities with Fivetran</span>
                    </div>
                    <fieldset class="data-stack-field-row" v-for="(value, key) in this.dataStackAndStaffing[this.reportType].engineeringFunction">
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
                    <div class="data-stack-field-row border-top">
                        <div>Total weekly pipeline maintenance time per engineer</div>
                        <div class="output-wrapper">
                            <output>
                                <span class="denom-hours">{{ totalWeeklyMaintainanceTimeWithoutFivetran }}</span>
                            </output>
                        </div>
                        <div class="output-wrapper">
                            <output>
                                <span class="denom-hours">{{ totalWeeklyMaintainanceTimeWithFivetran }}</span>
                            </output>
                        </div>
                    </div>
                </div>

                <!-- Additional comparison rows, render for saas and databases -->
                <div class="data-stack-staffing-field-group">
                    <div class="table-header three-column">
                        <span class="input-table-header text-left">Additional comparisons</span>
                        <span class="input-table-header text-right">Costs without Fivetran</span>
                        <span class="input-table-header text-right">Costs with Fivetran</span>
                    </div>
                    <fieldset class="data-stack-field-row" v-for="(value, key) in this.dataStackAndStaffing[this.reportType].additionalComparisons">
                        <div>{{ sentencize(key) }}</div>
                        <div class="input-label-caption">
                            <label :for="`${kebabize(key)}`"><i>{{ value.withoutFivetranLabel }}</i></label>
                            <input type="number" :for="`${kebabize(key)}`" :id="`${kebabize(key)}`" v-model="value.withoutFivetran" :defaultValue="value.withoutFivetran">
                        </div>
                        <div class="input-label-caption">
                            <label :for="`${kebabize(key)}`"><i>{{ value.withFivetranLabel }}</i></label>
                            <input type="number" v-model="value.withFivetran" :defaultValue="value.withFivetran">
                        </div>
                    </fieldset>
                </div>

                <!-- Additional cost inputs, render only for database -->
                <fieldset class="database-additional-cost-inputs" v-if="this.reportType === 'databases'">
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

            <!-- Generate report button -->
            <input type="submit" value="Generate report" id="generate-report" @click="submitForm">

        </form>
        
        
        <!-- Begin report -->
        <div class="form-block report" v-if="complete">

            <!-- Report header -->
            <div class="heading-block">
                <hgroup>
                    <h2>{{ reportOutputs.companyDetails.companyName }}</h2>
                    <p> Fivetran SaaS Connectors - ROI Analysis</p>
                    <p>Generated {{ new Date().toLocaleDateString("en-US") }}</p>
                    <p>Questions? Contact {{ reportOutputs.companyDetails.fivetranContactEmail }}</p>
                </hgroup>
                <div>
                    <img src="https://uploads-ssl.webflow.com/65ccfe0bfacd7e43c72090d6/65cd01136286d65c8f9a20cf_fivetran.svg">
                    <span>fivetran.com</span>
                </div>
            </div>

            <!-- First report section, "activities to build and maintain pipelines" -->
            <section>
                <!-- First section header -->
                <div class="table-header four-column">
                    <span class="input-table-header text-left">Activities to build & maintain pipelines</span>
                    <span class="input-table-header text-center">Current costs</span>
                    <span class="input-table-header text-center">Costs with Fivetran</span>
                    <span class="input-table-header text-center">Fivetran cost savings<span class="annotation"><br>(Current costs less costs w/Fivetran)</span></span>
                </div>
                
                <!-- Annual cost of building pipelines row -->
                <div class="table-row four-column">
                    <span class="input-table-header text-left">Annual cost of building pipelines</span>
                    <span class="input-table-header text-center">{{ this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostOfBuildingPipelines.currentCosts }}</span>
                    <span class="input-table-header text-center">{{ this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostOfBuildingPipelines.costsWithFivetran  }}</span>
                    <span class="input-table-header text-center">{{ this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostOfBuildingPipelines.fivetranCostSavings }}</span>
                </div>

                <!-- Annual cost of maintaining pipelines row -->
                <div class="table-row four-column">
                    <span class="input-table-header text-left">Annual cost of maintaining pipelines</span>
                    <span class="input-table-header text-center">{{ this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostOfMaintainingPipelines.currentCosts }}</span>
                    <span class="input-table-header text-center">{{ this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostOfMaintainingPipelines.costsWithFivetran }}</span>
                    <span class="input-table-header text-center">{{ this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostOfMaintainingPipelines.fivetranCostSavings }}</span>
                </div>
                
                <!-- Annual cost of pipeline related infrastructure row -->
                <div class="table-row four-column">
                    <span class="input-table-header text-left">Annual cost of pipeline related infrastructure</span>
                    <span class="input-table-header text-center">{{ this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostsOfPipelineRelatedInfrastructure.currentCosts }}</span>
                    <span class="input-table-header text-center">{{ this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostsOfPipelineRelatedInfrastructure.costsWithFivetran }}</span>
                    <span class="input-table-header text-center">{{ this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostsOfPipelineRelatedInfrastructure.fivetranCostSavings }}</span>
                </div>
            </section>
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
    max-width: 1280px;
    display: flex;
    align-items: left;
    flex-direction: column;
    gap: 40px;
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
    border-bottom: 1px solid var(--gray-90) !important;
    padding: 0px 0px 12px 0px !important;
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

label,
.input-table-header {
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

.segmented-control {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    grid-column: 1 / span 12;
    margin-bottom: 48px;

    div {
        display: flex;
        flex-direction: row;
    }
}

.data-stack-staffing-field-group {
    grid-column: 1 / span 10;
    display: flex;
    flex-direction: column;
    gap: 16px;

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

.table-header,
.table-row {
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


.data-stack-field-row {
    display: grid;
    grid-template-columns: repeat(9, 1fr);
    gap: 16px;
    align-items: baseline;
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
        font-size: 12px;
        line-height: 16px;
        font-weight: 400;
        text-align: right;
        flex: 0 0 60%;
    }
}

.denom-hours:after {
    content: ' hrs'
}

.database-additional-cost-inputs {
    grid-column: 1 / span 8;
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
    align-self: start;
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
    display: flex !important;
    row-gap: 60px;
    flex-direction: column;
    align-items: center;
}

.heading-block {
    display: flex;
    justify-content: space-between;

    hgroup,
    div {
        display: flex;
        flex-direction: column;
        gap: 6px;

        * {
            margin: 0;
            padding: 0;
        }
    }
    div {
        align-items: end;
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

.grid-child-span-3 {
    grid-column: auto / span 3;
}

.controls > * {
    margin-bottom: 36px;
}

.border-top {
    padding-top: 12px;
    border-top: 1px solid var(--gray-90);
}

.report > section {
    display: flex;
    flex-direction: column;
    gap: 16px;
}

</style>