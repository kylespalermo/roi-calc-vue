<script>
//default value appears to be unecessary when using v-model
export default {
    data() {
        return {
            labels: {
                fivetranContractPeriod: 'Fivetran contract period (months)',
                estimatedOnboardingTime: 'Estimated onboarding time (months)',
                averageSalary: 'Average salary (USD)'
            },
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
                            withoutFivetran: null,
                            withoutFivetranLabel: 'Researching APIs, writing new code',
                            withFivetran: null,
                            withFivetranLabel: 'Adding new connectors in Fivetran'
                        },
                        buildingTransformations: {
                            withoutFivetran: null,
                            withoutFivetranLabel: 'Building transformations for new models',
                            withFivetran: null,
                            withFivetranLabel: 'Building new models with Fivetran packages where possible',
                        },
                        maintainingIntegrations: {
                            withoutFivetran: null,
                            withoutFivetranLabel: 'Updating API versions, adding new fields, fixing bugs',
                            withFivetran: null,
                            withFivetranLabel: 'Monitoring Fivetran pipeline health'
                        },
                        maintainingTransformations: {
                            withoutFivetran: null,
                            withoutFivetranLabel: 'Adding transformations for existing models',
                            withFivetran: null,
                            withFivetranLabel: 'Fivetran managed packages - you just need to maintain custom code',
                        },
                        deploymentAndOrchestration: {
                            withoutFivetran: null,
                            withoutFivetranLabel: 'Promoting changes through dev/test, Co-ordinating pipeline runs',
                            withFivetran: null,
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
                    },
                    additionalCostInputs: {
                        costOfFivetran: null,
                    }
                },
                databases: {
                    engineeringFunction: {
                        totalBuildTimePerEngineer: {
                            withoutFivetran: null,
                            withoutFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',
                            withFivetran: null,
                            withFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',
                        },
                        maintenanceTimePerEngineer: {
                            withoutFivetran: null,
                            withoutFivetranLabel: 'Eque porro quisquam est qui dolorem ipsum quia.',
                            withFivetran: null,
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
                            withoutFivetran: null,//input an industry average here?
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
                        costOfDataDowntimePerHour: null,//need to input a default here?
                        costOfAlternative: null,//need to input a default here?
                        costOfFivetran: null,
                    }
                }
            },
            reportOutputs: {
                companyDetails: {
                    companyName: '',
                    prospectiveCustomerEmail: '',
                    fivetranContactEmail: '',
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
                    },
                    costOfAlternative: {
                        currentCosts: '',
                        costsWithFivetran: '',
                        fivetranCostSavings: ''
                    },
                    costOfDestination: {
                        currentCosts: '',
                        costsWithFivetran: '',
                        fivetranCostSavings: ''
                    },
                    costOfDataDowntime: {
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
                costOfFivetran: '',
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

            //if else to accomodate different keys in each report type
            if (this.reportType == "saas") {
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
            //structure for "Fivetran cost savings", always the 3rd key/value in the object, is "current costs - costs with Fivetran"
            //could probably refactor this to just make a deep copy of the original data object, if we cleaned up that structure

            //shorten the reference to report output object to make them more readable
            let r = this.reportOutputs;

            //update companyDetails 
            r.companyDetails.companyName = this.companyDetails.companyName;
            r.companyDetails.prospectiveCustomerEmail = this.companyDetails.prospectiveCustomerEmail;
            r.companyDetails.fivetranContactEmail = this.companyDetails.fivetranContactEmail;

            //update activities to build and maintain pipelines
            //annual cost of building pipelines
            r.activitiesToBuildAndMaintainPipelines.annualCostOfBuildingPipelines.currentCosts = this.calculateBuildMaintainCosts.annualCostOfBuildingPipelines.currentCosts;
            r.activitiesToBuildAndMaintainPipelines.annualCostOfBuildingPipelines.costsWithFivetran = this.calculateBuildMaintainCosts.annualCostOfBuildingPipelines.costsWithFivetran;
            r.activitiesToBuildAndMaintainPipelines.annualCostOfBuildingPipelines.fivetranCostSavings = this.calculateBuildMaintainCosts.annualCostOfBuildingPipelines.currentCosts - this.calculateBuildMaintainCosts.annualCostOfBuildingPipelines.costsWithFivetran;

            //update annuual cost of maintaining pipelines
            r.activitiesToBuildAndMaintainPipelines.annualCostOfMaintainingPipelines.currentCosts = this.calculateBuildMaintainCosts.annualCostOfMaintainingPipelines.currentCosts;
            r.activitiesToBuildAndMaintainPipelines.annualCostOfMaintainingPipelines.costsWithFivetran = this.calculateBuildMaintainCosts.annualCostOfMaintainingPipelines.costsWithFivetran;
            r.activitiesToBuildAndMaintainPipelines.annualCostOfMaintainingPipelines.fivetranCostSavings = this.calculateBuildMaintainCosts.annualCostOfMaintainingPipelines.currentCosts - this.calculateBuildMaintainCosts.annualCostOfMaintainingPipelines.costsWithFivetran;

            //annual cost of pipeline related infrastructure
            r.activitiesToBuildAndMaintainPipelines.annualCostsOfPipelineRelatedInfrastructure.currentCosts = this.dataStackAndStaffing[this.reportType].additionalComparisons.annualCostsOfPipelineRelatedInfrastructure.withFivetran;
            r.activitiesToBuildAndMaintainPipelines.annualCostsOfPipelineRelatedInfrastructure.costsWithFivetran = this.dataStackAndStaffing[this.reportType].additionalComparisons.annualCostsOfPipelineRelatedInfrastructure.withoutFivetran;
            r.activitiesToBuildAndMaintainPipelines.annualCostsOfPipelineRelatedInfrastructure.fivetranCostSavings = this.dataStackAndStaffing[this.reportType].additionalComparisons.annualCostsOfPipelineRelatedInfrastructure.withoutFivetran - this.dataStackAndStaffing[this.reportType].additionalComparisons.annualCostsOfPipelineRelatedInfrastructure.withFivetran;

            //databases only: cost of alternative
            r.activitiesToBuildAndMaintainPipelines.costOfAlternative.currentCosts = this.dataStackAndStaffing[this.reportType].additionalCostInputs.costOfAlternative;
            r.activitiesToBuildAndMaintainPipelines.costOfAlternative.costsWithFivetran = 0;
            r.activitiesToBuildAndMaintainPipelines.costOfAlternative.fivetranCostSavings = r.activitiesToBuildAndMaintainPipelines.costOfAlternative.currentCosts - r.activitiesToBuildAndMaintainPipelines.costOfAlternative.costsWithFivetran;

            //databases only: cost of destination
            r.activitiesToBuildAndMaintainPipelines.costOfDestination.currentCosts = this.dataStackAndStaffing[this.reportType].additionalComparisons.costOfDestination.withoutFivetran;
            r.activitiesToBuildAndMaintainPipelines.costOfDestination.costsWithFivetran = this.dataStackAndStaffing[this.reportType].additionalComparisons.costOfDestination.withFivetran;
            r.activitiesToBuildAndMaintainPipelines.costOfDestination.fivetranCostSavings = r.activitiesToBuildAndMaintainPipelines.costOfDestination.currentCosts - r.activitiesToBuildAndMaintainPipelines.costOfDestination.costsWithFivetran;

            //databases only: cost of data downtime
            const hrsPerYear = 24*365;
            r.activitiesToBuildAndMaintainPipelines.costOfDataDowntime.currentCosts = hrsPerYear * this.dataStackAndStaffing[this.reportType].additionalCostInputs.costOfDataDowntimePerHour * (1 - (this.dataStackAndStaffing[this.reportType].additionalComparisons.dataUptime.withoutFivetran * .01))
            r.activitiesToBuildAndMaintainPipelines.costOfDataDowntime.costsWithFivetran = hrsPerYear * this.dataStackAndStaffing[this.reportType].additionalCostInputs.costOfDataDowntimePerHour * (1 - (this.dataStackAndStaffing[this.reportType].additionalComparisons.dataUptime.withFivetran * .01))
            r.activitiesToBuildAndMaintainPipelines.costOfDataDowntime.fivetranCostSavings =  r.activitiesToBuildAndMaintainPipelines.costOfDataDowntime.currentCosts - r.activitiesToBuildAndMaintainPipelines.costOfDataDowntime.costsWithFivetran;

            //costOfEnvironment
            const costs = Object.values(r.activitiesToBuildAndMaintainPipelines)

            r.costOfEnvironment.currentCosts = costs.reduce((total, obj) => obj.currentCosts + total,0)
            r.costOfEnvironment.costsWithFivetran = costs.reduce((total, obj) => obj.costsWithFivetran + total,0)
            //field below is just a calculation of the two above in same object, so I'm calculating using the reportOutputs values
            //this avoids calling reduce again, but differs from the structure in the other sum/subtract operations above in this function (generally last of three in each)
            //so maybe refactor those above
            r.costOfEnvironment.fivetranCostSavings = r.costOfEnvironment.currentCosts - r.costOfEnvironment.costsWithFivetran;
            
            //cost of Fivetran
            r.costOfFivetran = this.dataStackAndStaffing[this.reportType].additionalCostInputs.costOfFivetran

            //final savings analysis
            //first value is just a copy of cost of environment, they're the same figure
            //see note above on structure/refactoring
            r.finalSavingsAnalysis.currentCosts = r.costOfEnvironment.currentCosts;
            //second value subtracts cost of Fivetran from cost of environment
            r.finalSavingsAnalysis.costsWithFivetran = r.costOfEnvironment.costsWithFivetran + r.costOfFivetran;
            r.finalSavingsAnalysis.fivetranCostSavings = r.costOfEnvironment.costsWithFivetran - r.costOfFivetran;
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
                            <label :for="`${kebabize(key)}`">{{ this.labels[key] }}</label>
                            <input type="number" v-model="fivetranEngagementTimeline[key]" :defaultValue="value" :step="key === 'fivetranContractPeriod' ? 12 : 1">
                        </div>
                    </div>
                </fieldset>
                <fieldset>
                    <legend>Current staffing costs</legend>
                    <div class="input-row">
                        <div class="input-label-box-horiz">
                            <label :for="`${kebabize('averageSalary')}`">{{ this.labels.averageSalary }}</label>
                            <input type="number" v-model="currentStaffingCosts.averageSalary" :defaultValue="currentStaffingCosts.averageSalary" step="1000">
                        </div>
                        <div class="input-label-box-horiz">
                            <label :for="`${kebabize('equivalentHourlyRate')}`">{{ sentencize('equivalentHourlyRate') }}</label>
                            <output :for="`${kebabize('equivalentHourlyRate')}`" :value="equivalentHourlyRate"><span class="output-denom-dollar">{{ equivalentHourlyRate }}</span></output>
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
                            <input type="number" :name="`${kebabize(key)}`" :id="`${kebabize(key)}`" v-model="value.withoutFivetran" :defaultValue="value.withoutFivetran">
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
                <fieldset class="additional-cost-inputs">
                    <legend>Additional cost inputs</legend>
                    <div class="input-row">
                        <div v-for="(value, key) in this.dataStackAndStaffing[this.reportType].additionalCostInputs" class="input-label-box-horiz">
                            <label :for="`${kebabize(key)}`">{{ sentencize(key) }}</label>
                            <input type="number" :id="`${kebabize(key)}`" :name="`${kebabize(key)}`" v-model="this.dataStackAndStaffing[reportType].additionalCostInputs[key]">
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
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostOfBuildingPipelines.currentCosts) }}</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostOfBuildingPipelines.costsWithFivetran)  }}</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostOfBuildingPipelines.fivetranCostSavings) }}</span>
                </div>

                <!-- Annual cost of maintaining pipelines row -->
                <div class="table-row four-column">
                    <span class="input-table-header text-left">Annual cost of maintaining pipelines</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostOfMaintainingPipelines.currentCosts) }}</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostOfMaintainingPipelines.costsWithFivetran) }}</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostOfMaintainingPipelines.fivetranCostSavings) }}</span>
                </div>
                
                <!-- Annual cost of pipeline related infrastructure row -->
                <div class="table-row four-column row-last-of-category">
                    <span class="input-table-header text-left">Annual cost of pipeline related infrastructure</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostsOfPipelineRelatedInfrastructure.currentCosts) }}</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostsOfPipelineRelatedInfrastructure.costsWithFivetran) }}</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.annualCostsOfPipelineRelatedInfrastructure.fivetranCostSavings) }}</span>
                </div>

                <!-- Databases report only, Cost of alternative -->
                <div v-if="this.reportType==='databases'" class="table-row four-column row-last-of-category">
                    <span class="input-table-header text-left">Cost of alternative (licensing/compute)</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.costOfAlternative.currentCosts) }}</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.costOfAlternative.costsWithFivetran) }}</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.costOfAlternative.fivetranCostSavings) }}</span>
                </div>

                <!-- Databases report only, Cost of destination -->
                <div v-if="this.reportType==='databases'" class="table-row four-column row-last-of-category">
                    <span class="input-table-header text-left">Cost of destination (i.e. ingestion costs)</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.costOfDestination.currentCosts) }}</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.costOfDestination.costsWithFivetran) }}</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.costOfDestination.fivetranCostSavings) }}</span>
                </div>

                <!-- Databases report only, Cost of data downtime -->
                <div v-if="this.reportType==='databases'" class="table-row four-column row-last-of-category">
                    <span class="input-table-header text-left">Cost of data downtime</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.costOfDataDowntime.currentCosts) }}</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.costOfDataDowntime.costsWithFivetran) }}</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.activitiesToBuildAndMaintainPipelines.costOfDataDowntime.fivetranCostSavings) }}</span>
                </div>
                
                <!-- end of this group of lines, begin a new one -->

                <!-- Cost of environment row -->
                <div class="table-row four-column">
                    <span class="input-table-header text-left">Cost of environment</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.costOfEnvironment.currentCosts) }}</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.costOfEnvironment.costsWithFivetran) }}</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.costOfEnvironment.fivetranCostSavings) }}</span>
                </div>
                
                <!-- Cost of Fivetran row -->
                <div class="table-row four-column row-last-of-category">
                    <span class="input-table-header text-left">Cost of Fivetran</span>
                    <!-- current costs field not applicable, so displays dash -->
                    <span class="input-table-header text-center">&ndash;</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.costOfFivetran) }}</span>
                    <!-- field below renders in parens to show a negative value -->
                    <span class="input-table-header text-center">({{ this.formatDollars(this.reportOutputs.costOfFivetran) }})</span>
                </div>

                <!-- Totals row -->
                <div class="table-row four-column row-totals">
                    <span class="input-table-header text-left">Final savings analysis</span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.finalSavingsAnalysis.currentCosts) }}<span class="annotation"><br>Total existing costs</span></span>
                    <span class="input-table-header text-center">{{ this.formatDollars(this.reportOutputs.finalSavingsAnalysis.costsWithFivetran) }}<span class="annotation"><br>Total costs with Fivetran</span></span>
                    <span class="input-table-header text-center"><em>{{ this.formatDollars(this.reportOutputs.finalSavingsAnalysis.fivetranCostSavings) }}</em><br><span class="annotation">Annual savings realized with Fivetran</span></span>
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

.output-denom-dollar::before {
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

.additional-cost-inputs {
    grid-column: 1 / span 10;
    display: flex;
    .input-row {
        grid-column: auto / span 9;
    }
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

.row-last-of-category {
    border-color: var(--gray-90);
    margin-bottom: 12px;
}

.row-totals {
    border: none;
    background: var(--citron-10);
    margin-left: -20px;
    margin-right: -20px;
    padding: 20px;
    border-radius: 4px;
    font-size: 16px;
}

.row-totals em {
    font-weight: 800;
    text-decoration: none;
    font-style: normal;
}

</style>