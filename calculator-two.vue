<script>
//TO DO:
//1. BUILD IN MIN & MAX VALUES

//default value appears to be unecessary when using v-model
export default {
    data() {
        return {
            showTransformations: false,
            showWorkSchedule: false,
            showIDCInputs: false,
            reportOutputs: {},
            reportSums: {},
            reportComplete: false,
            contactInformation: {
                companyName: {
                    annotation: 'Company name',
                    required: true,
                    value: ''
                },

                // prospectiveCustomerEmail: {
                //     annotation: 'Prospective customer email',
                //     required: true,
                //     value: ''
                // },

                fivetranContactEmail: {
                    annotation: 'Fivetran contact email',
                    required: true,
                    value: ''
                },
            },

            //current staffing costs
            averageSalary: {
                required: true,
                value: 70000,
                increment: 1000,
                annotation: 'Average salary ($)',
                min: 1000,
            },

            workSchedule: {
                //work schedule
                hoursWorkedPerWeek: {
                    required: true,
                    value: 40,
                    annotation: 'Hours worked per week',
                    min: 1,
                    max: 72
                },

                weeksWorkedPerYear: {
                    required: true,
                    value: 48,
                    annotation: 'Weeks worked per year',
                    min: 1,
                    max: 52
                },
            },

            //data integration cost and maintenance

            numberOfEngineers: {
                required: true,
                value: 1,
                annotation: 'Number of engineers',
                min: 1
            },

            //pipelines inputs
            pipelines: {
                building: {
                    currentState: {
                        value: 0,
                        annotation: 'Researching APIs, database documentation, code development.'
                    },
                    withFivetran: {
                        value: 0,
                        annotation: 'Adding new connectors in Fivetran.'
                    }
                },
                uptimeMaintenance: {
                    currentState: {
                        value: 0,
                        annotation: 'Updating API/Database versions, fixing bugs.'
                    },
                    withFivetran: {
                        value: 0,
                        annotation: 'Monitoring Fivetran pipeline health.'
                    }
                },
                schemaChangeMaintenance: {
                    currentState: {
                        value: 0,
                        annotation: 'Managing new field additions, deletions, data type changes.'
                    },
                    withFivetran: {
                        value: 0,
                        annotation: 'Fivetran automated schema migration.'
                    }
                },
                deploymentAndOrchestration: {
                    currentState: {
                        value: 0,
                        annotation: 'Promoting changes through dev/test, Co-ordinating pipeline runs.'
                    },
                    withFivetran: {
                        value: 0,
                        annotation: 'Fivetran API scheduler.'
                    }
                }
            },
            
            //transformations inputs
            transformations: {
                building: {
                    currentState: {
                        value: 0,
                        annotation: 'Building transformations for new models.'
                    },
                    withFivetran: {
                        value: 0,
                        annotation: 'Building new models with Fivetran packages where possible.'
                    }
                },
                modelMaintenance: {
                    currentState: {
                        value: 0,
                        annotation: 'Updating transformations for existing models.'
                    },
                    withFivetran: {
                        value: 0,
                        annotation: 'Fivetran managed packages - you just need to maintain custom code.'
                    }
                },
                deploymentAndOrchestration: {
                    currentState: {
                        value: 0,
                        annotation: 'Promoting changes through dev/test, Co-ordinating transformation runs.',
                        increment: 1000
                    },
                    withFivetran: {
                        value: 0,
                        annotation: 'Fivetran transformations scheduler.',
                        increment: 1000
                    }
                }
            },

            //additional comparisions and costs
            infrastructureCosts: {
                currentState: {
                    value: 0,
                    annotation: 'VMs/networking/scheduler costs for running pipelines/transformations.',
                    increment: 1000
                },
                withFivetran: {
                    value: 0,
                    annotation: 'Reduced costs with Fivetran.',
                    increment: 1000
                }
            },
            dataUptime: {
                currentState: {
                    value: 99.9,
                    annotation: 'Costs associated with Data Downtime e.g. lost orders from data pipeline bugs.',
                    increment: .01
                },
                withFivetran: {
                    value: 99.99,
                    annotation: 'Reduced downtime with Fivetran',
                    increment: .01
                }
            },
            destinationIngestionCosts: {
                currentState: {
                    value: 0,
                    annotation: 'Data warehouse/lake ingestion costs with current solution.',
                    increment: 1000
                },
                withFivetran: {
                    value: 0,
                    annotation: 'Reduced deestination ingestion costs with Fivetran',
                    increment: 1000
                }
            },
            costOfSolution: {
                currentState: {
                    value: 0,
                    annotation: 'Cost of alternative/incumbent solution.',
                    increment: 1000
                },
                withFivetran: {
                    value: 0,
                    annotation: 'Cost of Fivetran',
                    increment: 1000
                }
            },

            //single-value inputs, last in data integration cost and maintenance section
            costOfDataDowntimePerHour: {
                value: 0,
                annotation: '$',
                increment: 1000,
            },

            additionalCosts: {
                value: 0,
                annotation: 'annual, $',
            },

            //productivity gains by function section
            idcWorkFunctions: {
                dataEngineers: {
                    equivalentProductivityLevel: { value: 0 },
                    salary: { value: 70000 },
                    productivityGain: { value: 0.48 },
                    include: { value: false },
                },
                dataAnalytics: {
                    equivalentProductivityLevel: { value: 0 },
                    salary: { value: 70000 },
                    productivityGain: { value: 0.02 },
                    include: { value: false },
                },
                dataGovernance: {
                    equivalentProductivityLevel: { value: 0 },
                    salary: { value: 70000 },
                    productivityGain: { value: 0.16 },
                    include: { value: false },
                },
                finance: {
                    equivalentProductivityLevel: { value: 0 },
                    salary: { value: 70000 },
                    productivityGain: { value: 0.40 },
                    include: { value: false },
                },
                productManagement: {
                    equivalentProductivityLevel: { value: 0 },
                    salary: { value: 70000 },
                    productivityGain: { value: 0.12 },
                    include: { value: false },
                },
                salesAndCustomerSuccess: {
                    equivalentProductivityLevel: { value: 0 },
                    salary: { value: 70000 },
                    productivityGain: { value: 0.19 },
                    include: { value: false },
                },
                logistics: {
                    equivalentProductivityLevel: { value: 0 },
                    salary: { value: 70000 },
                    productivityGain: { value: 0.29 },
                    include: { value: false },
                },
                marketing: {
                    equivalentProductivityLevel: { value: 0 },
                    salary: { value: 70000 },
                    productivityGain: { value: 0.16 },
                    include: { value: false },
                }
            },

            //Overall revenue gains and operational efficiency section
            revenueGains: {
                additionalGrossRevenue: { value: 554894 },
                //margin is a percentage, but we're storing as int. So "15" = "15%". Solve in future w/custom input.
                margin: { value: 15 },
                include: { value: false },
            },

            operationalCostSavings: {
                oneTime: { value: 285714 },
                annual: { value: 177400 },
                include: { value: false },
            }
        }
    },
    computed: {
        //calculates an hourly rate based on average salary and work schedule inputs in staffing costs section
        equivalentHourlyRate() {
            return this.averageSalary.value / (this.workSchedule.weeksWorkedPerYear.value * this.workSchedule.hoursWorkedPerWeek.value)
        },
        //displayed beneath pipelines/transformations inputs
        //sums hours in before and after Fivetran scenarios for both categories
        totalTime() {
            let pipelines = Object.values(this.pipelines);
            let transformations = Object.values(this.transformations);

            let totalCurrentPipelineHours = pipelines.reduce((total, obj) => obj.currentState.value + total, 0);
            let totalFivetranPipelineHours = pipelines.reduce((total, obj) => obj.withFivetran.value + total, 0);

            let totalCurrentTransformationsHours = transformations.reduce((total, obj) => obj.currentState.value + total, 0);
            let totalFivetranTransformationsHours = transformations.reduce((total, obj) => obj.withFivetran.value + total, 0);

            let currentState = (totalCurrentPipelineHours + totalCurrentTransformationsHours) * this.numberOfEngineers.value;
            let withFivetran = (totalFivetranPipelineHours + totalFivetranTransformationsHours) * this.numberOfEngineers.value;

            return {
                currentState: currentState,
                withFivetran: withFivetran
            }
        },

        //the following three computed properties are, semantically, children of other data objects
        //could attempt to refactor these as watchers, allowing you to call them from the main data object they're associated with.
        //for example, operationalCostSavings.averageAnnualSaving. Trouble is calling method from within a data() object passing data() stuff as arg
        //you'd need to move some of that data outside of data() in order to call it

        //returns a before and after Fivetran scenario and total savings for each IDC work function
        idcProductivityGains(){
            let idcProductivityGains = {};
            for (const key in this.idcWorkFunctions) {
                idcProductivityGains[key] = this.calculateIDCGains(this.idcWorkFunctions[key].salary.value, this.idcWorkFunctions[key].equivalentProductivityLevel.value, this.idcWorkFunctions[key].productivityGain.value)
                }
            return idcProductivityGains;
        },

        //associated with Revenue Gains line, second-to-last IDC input
        annualNetGain() {
            return this.revenueGains.additionalGrossRevenue.value * (this.revenueGains.margin.value/100);
        },
        
        //associated with Operational Cost Savings line, last IDC input
        averageAnnualSaving() {
            return this.operationalCostSavings.oneTime.value + this.operationalCostSavings.annual.value
        }
        
    },
    methods: {
        calculateIDCGains(salary, equivalentProductivityLevel, productivityGain) {
            let currentState = salary * equivalentProductivityLevel;
            let withFivetran = (currentState * productivityGain) + currentState;
            let averageAnnualGain = withFivetran - currentState;
            return {
                currentState: currentState,
                withFivetran: withFivetran,
                averageAnnualGain: averageAnnualGain
            }
        },
        calculateCostSavings(currentState, withFivetran) {
            return currentState - withFivetran;
        },
        sentencize(str) {
            let sentence = str.replace(/[A-Z]+(?![a-z])|[A-Z]/g, ($, ofs) => (ofs ? " " : "") + $.toLowerCase())
            return sentence.charAt(0).toUpperCase() + sentence.slice(1);
        },
        formatDollars(num) {
            const numOptions = { style: 'currency', currency: 'USD' };
            const numberFormat = new Intl.NumberFormat('en-US', numOptions);

            return numberFormat.format(num)
        },
        calculateDataIntegrationCostAndMaintenance(...keys){

            let currentStateHours = 0;
            let withFivetranHours = 0;

            keys.forEach(key => {
                currentStateHours += this.findAllByKey(key, "currentState").reduce((total, obj) => obj.value + total, 0);
                withFivetranHours += this.findAllByKey(key, "withFivetran").reduce((total, obj) => obj.value + total, 0);
            });

            if (currentStateHours + withFivetranHours === 0) {
                return null;
            }

            let currentState = currentStateHours * this.workSchedule.weeksWorkedPerYear.value * this.equivalentHourlyRate;
            let withFivetran = withFivetranHours * this.workSchedule.weeksWorkedPerYear.value * this.equivalentHourlyRate;
            let costSavings = this.calculateCostSavings(currentState, withFivetran)
            
            return {
                currentState: currentState,
                withFivetran: withFivetran,
                costSavings: costSavings
            }
        },
        findAllByKey(obj, keyToFind) {
            return Object.entries(obj)
                .reduce((acc, [key, value]) => (key === keyToFind)
                ? acc.concat(value)
                : (typeof value === 'object')
                ? acc.concat(this.findAllByKey(value, keyToFind))
                : acc
            , [])
        },
        calculateCostOfDataDowntime(){
            let hoursPerYear = 24*365;

            if (this.costOfDataDowntimePerHour.value === 0) {
                return null;
            }
            
            let currentState = hoursPerYear * this.costOfDataDowntimePerHour.value * (1 - (this.dataUptime.currentState.value * .01));
            let withFivetran = hoursPerYear * this.costOfDataDowntimePerHour.value * (1 - (this.dataUptime.withFivetran.value * .01));
            let costSavings = this.calculateCostSavings(currentState, withFivetran);

            return {
                currentState: currentState,
                withFivetran: withFivetran,
                costSavings: costSavings
            }
        },
        formatInputsValueForReport(obj) {

            let currentState = obj.currentState.value;
            let withFivetran = obj.withFivetran.value;

            if (currentState + withFivetran === 0) {
                return null;
            }

            return {
                currentState: obj.currentState.value,
                withFivetran: obj.withFivetran.value,
                costSavings: this.calculateCostSavings(obj.currentState.value, obj.withFivetran.value)
            }
        },
        sumReportLines(lines, keys = ['currentState', 'withFivetran', 'costSavings']){

            let currentState = 0;
            let withFivetran = 0;
            let costSavings = 0;
            
            for (let line in lines) {
                if (lines[line]) {
                    currentState += lines[line][keys[0]];
                    withFivetran += lines[line][keys[1]];
                    costSavings += lines[line][keys[2]];
                }
            }

            return {
                currentState: currentState,
                withFivetran: withFivetran,
                costSavings: costSavings
            }
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
                this.generateReport();
            }
        },
        generateReport() {
            this.reportOutputs.contactInformation = this.contactInformation,
            this.reportOutputs.dataIntegrationCostAndMaintenance = {
                buildingPipelines: this.calculateDataIntegrationCostAndMaintenance(this.pipelines.building),
                maintainingPipelines: this.calculateDataIntegrationCostAndMaintenance(this.pipelines.uptimeMaintenance, this.pipelines.schemaChangeMaintenance, this.pipelines.deploymentAndOrchestration),
                buildingTransformations: this.calculateDataIntegrationCostAndMaintenance(this.transformations.building),
                maintainingTransformations: this.calculateDataIntegrationCostAndMaintenance(this.transformations.modelMaintenance, this.transformations.deploymentAndOrchestration),
                infrastructureCosts: this.formatInputsValueForReport(this.infrastructureCosts),
                costOfDataDowntime: this.calculateCostOfDataDowntime(),
                destinationIngestion: this.formatInputsValueForReport(this.destinationIngestionCosts),
                costOfSolution: this.formatInputsValueForReport(this.costOfSolution),
                additionalCosts: this.formatInputsValueForReport({ currentState: { value: this.additionalCosts.value }, withFivetran: { value: 0 } }) 
            }

            for (let key in this.reportOutputs.dataIntegrationCostAndMaintenance) {
                if (this.reportOutputs.dataIntegrationCostAndMaintenance[key] === null) {
                    delete this.reportOutputs.dataIntegrationCostAndMaintenance[key]
                }
            }

            this.reportOutputs.idcProductivityGains = {}

            for (let key in this.idcWorkFunctions) {
                if (this.idcWorkFunctions[key].include.value) {
                    this.reportOutputs.idcProductivityGains[key] = this.idcProductivityGains[key]
                }
            }

            this.reportOutputs.idcRevenueGains = {}

            if (this.operationalCostSavings.include.value) { this.reportOutputs.idcRevenueGains.operationalCostSavings = this.averageAnnualSaving }
            if (this.revenueGains.include.value) { this.reportOutputs.idcRevenueGains.revenueGains = this.annualNetGain }

            this.reportSums.dataIntegrationCostAndMaintenance = this.sumReportLines(this.reportOutputs.dataIntegrationCostAndMaintenance);
            this.reportSums.idcProductivityGains = this.sumReportLines(this.reportOutputs.idcProductivityGains, ['currentState', 'withFivetran', 'averageAnnualGain']);
            this.reportSums.totalRevenueGain = {}
            this.reportSums.totalRevenueGain.costSavings = Object.values(this.reportOutputs.idcRevenueGains).reduce((a, b) => a + b, 0);
            
            this.reportOutputs.overallSavings = 0;
            for (let key in this.reportSums) {
                this.reportOutputs.overallSavings += this.reportSums[key].costSavings;
            }

            if (Object.keys(this.reportOutputs.dataIntegrationCostAndMaintenance).length === 0
            && Object.keys(this.reportOutputs.idcProductivityGains).length === 0
            && Object.keys(this.reportOutputs.idcRevenueGains).length === 0) {
                alert('Please enter some data to include in the report')    
            } else {
                this.reportComplete = true;
            }

        }
    }
}

</script>
<template>
    <div class="top-nav">
            <header>
                <a  href="https://www.fivetran.com/"><img src="https://uploads-ssl.webflow.com/65ccfe0bfacd7e43c72090d6/65cd01136286d65c8f9a20cf_fivetran.svg" alt="Fivetran logo"></a>
                <nav>
                    <ul>
                        <li><a href="https://fivetran.com/docs/getting-started" target="_blank">Docs</a></li>
                        <li><a href="https://fivetran.com/pricing" target="_blank">Pricing</a></li>
                        <li><a href="https://fivetran.com/login" target="_blank">Sign in</a></li>
                    </ul>
                </nav>
            </header>
        </div>
    <main>
        <form onsubmit="return false">
            <h1>Fivetran ROI Calculator</h1>
            <!-- first input block -->
            <section class="form-block" id="company-profile">
                <h2>Company profile</h2>
                <!-- contact information -->
                <fieldset class="flex-column" id="contact-information">
                    <legend class="row-header">Contact information</legend>
                    <div class="field-label" v-for="(value, key) in this.contactInformation">
                        <label :for=key :class="value.required ? 'required' : ''">{{ sentencize(key) }}</label>
                        <input v-model="value.value" :id=key type="text" required>
                    </div>
                </fieldset>
                <!-- current staffing costs -->
                <fieldset class="flex-row" id="current-staffing-costs">
                    <legend class="row-header">Current staffing costs</legend>
                    <div class="field-box">
                        <label>{{ this.averageSalary.annotation }}</label>
                        <input v-model="this.averageSalary.value" id="averageSalary" type="number" :min="this.averageSalary.min ? this.averageSalary.min : 0">
                    </div>
                    <div class="field-box">
                        <label>Equivalent hourly rate</label>
                        <output>{{ formatDollars(this.equivalentHourlyRate) }}</output>
                    </div>
                </fieldset>
                <!-- work schedule -->
                <fieldset class="flex-row" id="work-schedule">
                    <legend class="row-header collapsible-trigger" :class="showWorkSchedule ? 'active' : ''" @click="showWorkSchedule = !showWorkSchedule">Work schedule</legend>
                    <template v-if="showWorkSchedule">
                        <div v-for="(value, key) in this.workSchedule" class="field-box">
                            <label>{{ value.annotation }}</label>
                            <input v-model="value.value" :id="key" type="number" :min="value.min ? value.min : 0" :max="value.max ? value.max : 0">
                        </div>
                    </template>
                </fieldset>
            </section>

            <!-- Data integration cost and maintenance -->
            <section class="form-block" id="data-integration-cost-and-maintenance">
                <h2>Data integration cost and maintenance</h2>
                <div class="field-box" id="number-of-engineers">
                    <label>{{ numberOfEngineers.annotation }}</label>
                    <input v-model="numberOfEngineers.value" id="numberOfEngineers" type="number" :min="this.numberOfEngineers.min">
                </div>
                <!-- Pipelines -->
                <fieldset id="pipelines">
                    <div class="row-header">
                        <legend>Pipelines</legend>
                        <span>Current state (hrs/week)</span>
                        <span>With Fivetran (hrs/week)</span>
                    </div>
                    <div v-for="(value, key) in this.pipelines" class="input-row">
                        <label>{{ sentencize(key) }}</label>
                        <div v-for="(nestedValue, nestedKey) in value" class="annotated-input">
                            <label>{{ nestedValue.annotation }}</label>
                            <input v-model="nestedValue.value" :id=nestedKey min="0" type="number">
                        </div>
                    </div>
                </fieldset>
                <!-- Transformations -->
                <fieldset id="transformations">
                    <div class="row-header">
                        <legend class="collapsible-trigger" :class="showTransformations ? 'active' : ''" @click="showTransformations = !showTransformations">Transformations</legend>
                    </div>
                    <template v-if="showTransformations">
                        <div v-for="(value, key) in this.transformations" class="input-row">
                            <label>{{ sentencize(key) }}</label>
                            <div v-for="(nestedValue, nestedKey) in value" class="annotated-input">
                                <label>{{ nestedValue.annotation }}</label>
                                <input v-model="nestedValue.value" :id=nestedKey min="0" type="number">
                            </div>
                        </div>
                    </template>
                </fieldset>
                <div id="total-time">
                    <div class="label-like">Total time (hours)</div>
                    <div class="annotated-input">
                        <label></label>
                        <output>{{ this.totalTime.currentState }}</output>    
                    </div>
                    <div class="annotated-input">
                        <label></label>
                        <output>{{ this.totalTime.withFivetran }}</output>    
                    </div>
                </div>
                <!-- Additional comparisons and costs -->
                <fieldset id="additional-comparisons-and-costs">
                    <div class="row-header">
                        <legend>Additional comparisons and costs</legend>
                        <span>Current state</span>
                        <span>With Fivetran</span>
                    </div>
                    <div class="input-row">
                        <label>Infrastructure costs (annual, $)</label>
                        <div v-for="(nestedValue, nestedKey) in this.infrastructureCosts" class="annotated-input">
                            <label>{{ nestedValue.annotation }}</label>
                            <input v-model="nestedValue.value" :id=nestedKey min="0" type="number">
                        </div>
                    </div>
                    <div class="input-row">
                        <label>Data uptime (percent)</label>
                        <div v-for="(nestedValue, nestedKey) in this.dataUptime" class="annotated-input">
                            <label>{{ nestedValue.annotation }}</label>
                            <input v-model="nestedValue.value" :id=nestedKey min="0" type="number" step=".01">
                        </div>
                    </div>
                    <div class="input-row">
                        <label>Destination ingest costs (annual, $)</label>
                        <div v-for="(nestedValue, nestedKey) in this.destinationIngestionCosts" class="annotated-input">
                            <label>{{ nestedValue.annotation }}</label>
                            <input v-model="nestedValue.value" :id=nestedKey min="0" type="number">
                        </div>
                    </div>
                    <div class="input-row">
                        <label>Cost of solution (annual, $)</label>
                        <div v-for="(nestedValue, nestedKey) in this.costOfSolution" class="annotated-input">
                            <label>{{ nestedValue.annotation }}</label>
                            <input v-model="nestedValue.value" :id=nestedKey min="0" type="number">
                        </div>
                    </div>
                </fieldset>
                <!-- single-input-fields -->
                <div class="field-box" id="cost-of-data-downtime-per-hour">
                    <label>Cost of data downtime per hour ($)</label>
                    <input v-model="this.costOfDataDowntimePerHour.value" type="number" min="0">
                </div>
                <div class="field-box" id="additional-costs">
                    <label>Additional costs</label>
                    <input v-model="this.additionalCosts.value" type="number" min="0">
                </div>
            </section>

            <!-- business impact of Fivetran -->
            <section class="form-block" id="business-impact-of-fivetran">
                <h2 class="collapsible-trigger" :class="showIDCInputs ? 'active' : ''" @click="showIDCInputs = !showIDCInputs">Business impact of Fivetran (<a href="https://www.fivetran.com/blog/new-idc-analysis-the-value-of-fivetran-for-enterprise" target="_blank">per IDC research</a>)</h2>
                <!-- productivity gains with Fivetran -->
                <template v-if="this.showIDCInputs">
                    <div class="input-group">
                        <hgroup>
                            <h3>Productivity gains with Fivetran</h3>
                            <p>IDC conducted a recent study of Fivetran customers and found that study participants achieved benefits worth an average of $3,642,700 per organization over three years through more productive staff performance and business enablement.</p>
                        </hgroup>
                        <fieldset id="productivity-gains-with-fivetran">
                            <div class="row-header">
                                <legend>Productivity gains by function</legend>
                                <span>Equivalent productivity level (FTEs)</span>
                                <span>Salary</span>
                                <span>Productivity gain (%)</span>
                                <span>Average Annual Gain</span>
                                <span>Include?</span>
                            </div>
                            <div v-for="(value, key) in this.idcWorkFunctions" class="input-row">
                                <label>{{ sentencize(key) }}</label>
                                <input v-model="value.equivalentProductivityLevel.value" :id="`${key}_equivalentProductivityLevel`" min="0" type="number">
                                <input v-model="value.salary.value" :id="`${key}_salary`" min="0" type="number">
                                <div class="const-input" :id="`${key}_productivityGain`">{{ Math.round(value.productivityGain.value * 100) }}</div>
                                <output>{{ formatDollars(this.idcProductivityGains[key].averageAnnualGain) }}</output>
                                <input v-model="value.include.value" :id="`${key}_include`" type="checkbox">
                            </div>
                        </fieldset>
                    </div>
                    <!-- Overall revenue gains and operational efficiency -->
                    <div class="input-group" id="overall-revenue-gains-and-operational-efficiency">
                        <hgroup>
                            <h3>Overall revenue gains and operational efficiency</h3>
                            <p>Interviewed organizations attributed higher revenue to their use of Fivetran. Near-real-time access to high-quality data enabled interviewed organizations to better serve their customers, support products or business initiatives with data-backed insights, and plan more strategically.</p>
                        </hgroup>
                        <!-- revenue gains -->
                        <fieldset id="revenue-gains">
                            <div class="row-header">
                                <legend class="hidden">Revenue gains</legend>
                                <span>Additional gross revenue ($)</span>
                                <span>Margin (percent)</span>
                                <span>Annual net gain</span>
                                <span>Include?</span>
                            </div>
                            <div class="input-row">
                                <div class="label-like annotated-label">
                                    Revenue gains
                                    <p>Study participants were able to reduce bad technical debt and be more operationally resilient to business challenges - reducing overall operating costs.</p>
                                </div>
                                <input v-model="this.revenueGains.additionalGrossRevenue.value" id="revenueGains_oneTime" type="number" min="0">
                                <input v-model="this.revenueGains.margin.value" id="revenueGains_margin" type="number" min="0">
                                <output>{{ this.formatDollars(this.annualNetGain) }}</output>
                                <input v-model="this.revenueGains.include.value" id="revenueGains_include" type="checkbox">
                            </div>
                        </fieldset>
                        <!-- operational cost savings -->
                        <fieldset>
                            <div class="row-header">
                                <legend class="hidden">Operational cost savings</legend>
                                <span>One-time ($)</span>
                                <span>Annual</span>
                                <span>Average annual saving</span>
                                <span>Include?</span>
                            </div>
                            <div class="input-row">
                                <div class="label-like">Operational cost savings</div>
                                <input v-model="this.operationalCostSavings.oneTime.value" id="operationalCostSavings_oneTime" type="number" min="0">
                                <input v-model="this.operationalCostSavings.annual.value" id="operationalCostSavings_annual" type="number" min="0">
                                <output>{{ this.formatDollars(this.averageAnnualSaving) }}</output>
                                <input v-model="this.operationalCostSavings.include.value" id="operationalCostSavings_inlclude" type="checkbox">
                            </div>
                        </fieldset>
                    </div>
                </template>
            </section>
            <input type="submit" :value="this.reportComplete ? 'Update report' : 'Generate report'" id="generate-report" @click="submitForm">
        </form>

        <!-- report -->
        <section v-if="this.reportComplete" class="form-block report">
            <hgroup class="report-heading">
                <h2>
                    {{ this.reportOutputs.contactInformation.companyName.value }}
                    <p class="report-subhead">ROI analysis</p>
                </h2>
                <p>Generated {{ new Date().toLocaleDateString("en-US") }}</p>
                <p>Questions? Contact {{ this.reportOutputs.contactInformation.fivetranContactEmail.value }}</p>
            </hgroup>
            <div class="report-logo">
                <img src="https://uploads-ssl.webflow.com/65ccfe0bfacd7e43c72090d6/65cd01136286d65c8f9a20cf_fivetran.svg">
                <span>fivetran.com</span>
            </div>
            <!-- report section one -->
            <h3 v-if="Object.keys(this.reportOutputs.dataIntegrationCostAndMaintenance).length > 0">Data integration cost and maintenance (annual)</h3>
            <div v-if="Object.keys(this.reportOutputs.dataIntegrationCostAndMaintenance).length > 0" class="report-table-section">
                <div class="report-table-row row-header">
                    <span>Cost category</span>
                    <span>Current costs</span>
                    <span>Costs with Fivetran</span>
                    <span>Cost savings</span>
                </div>
                <template v-for="(value, key) in this.reportOutputs.dataIntegrationCostAndMaintenance">
                    <div v-if="value" class="report-table-row">
                        <span>{{ sentencize(key) }}</span>
                        <span>{{ this.formatDollars(value.currentState) }}</span>
                        <span>{{ this.formatDollars(value.withFivetran) }}</span>
                        <span>{{ this.formatDollars(value.costSavings) }}</span>
                    </div>
                </template>
                <div class="total-wrapper report-table-row">
                    <span>Total</span>
                    <span>{{ this.formatDollars(this.reportSums.dataIntegrationCostAndMaintenance.currentState) }}</span>
                    <span>{{ this.formatDollars(this.reportSums.dataIntegrationCostAndMaintenance.withFivetran) }}</span>
                    <span>{{ this.formatDollars(this.reportSums.dataIntegrationCostAndMaintenance.costSavings) }}</span>
                </div>
            </div>
            <!-- report section two -->
            <h3 v-if="Object.keys(this.reportOutputs.idcProductivityGains).length > 0 || Object.keys(this.reportOutputs.idcRevenueGains).length > 0" >Business impact of Fivetran (<a href="https://www.fivetran.com/blog/new-idc-analysis-the-value-of-fivetran-for-enterprise" target="_blank">per IDC research</a>)</h3>
            <div v-if="Object.keys(this.reportOutputs.idcProductivityGains).length > 0" class="report-table-section">
                <div class="report-table-row row-header">
                    <span>Productivity gains</span>
                    <span>Before Fivetran</span>
                    <span>After Fivetran</span>
                    <span>Productivity gains after Fivetran</span>
                </div>
                <div v-for="(value, key) in this.reportOutputs.idcProductivityGains" class="report-table-row">
                    <span>{{ sentencize(key) }}</span>
                    <span>{{ this.formatDollars(value.currentState) }}</span>
                    <span>{{ this.formatDollars(value.withFivetran) }}</span>
                    <span>{{ this.formatDollars(value.averageAnnualGain) }}</span>
                </div>
                <div class="total-wrapper report-table-row">
                    <span>Total</span>
                    <span>{{ this.formatDollars(this.reportSums.idcProductivityGains.currentState) }}</span>
                    <span>{{ this.formatDollars(this.reportSums.idcProductivityGains.withFivetran) }}</span>
                    <span>{{ this.formatDollars(this.reportSums.idcProductivityGains.costSavings) }}</span>
                </div>
            </div>
            <!-- report section three -->
            <div v-if="Object.keys(this.reportOutputs.idcRevenueGains).length > 0" class="report-table-section">
                <div class="report-table-row row-header two-col">
                    <span>Overall revenue gains and operational efficiency</span>
                    <span>Average annual gain</span>
                </div>
                <div v-if="this.reportOutputs.idcRevenueGains.revenueGains" class="report-table-row two-col">
                    <span>Revenue gains</span>
                    <span>{{ this.formatDollars(this.reportOutputs.idcRevenueGains.revenueGains) }}</span>
                </div>
                <div v-if="this.reportOutputs.idcRevenueGains.operationalCostSavings" class="report-table-row two-col">
                    <span>Operational cost savings</span>
                    <span>{{ this.formatDollars(this.reportOutputs.idcRevenueGains.operationalCostSavings) }}</span>
                </div>
                <div class="total-wrapper report-table-row two-col">
                    <span>Total</span>
                    <span>{{ this.formatDollars(this.reportSums.totalRevenueGain.costSavings) }}</span>
                </div>
            </div>
            <div class="total-wrapper report-table-row two-col grand-total">
                <span>Overall benefit</span>
                <span>{{ this.formatDollars(this.reportOutputs.overallSavings) }}</span>
            </div>
        </section>

        <div v-if="this.reportComplete" id="print-button">
            <button onclick="window.print()">Print report</button>
        </div>
    </main>
</template>

<style>

.grand-total {
    background: var(--blue-60) !important;
    font-weight: 600 !important;
    border: unset !important;
    grid-area: 6;
}

.grand-total span {
    color: white !important;
    font-size: 18px;
    line-height: 24px;
    font-weight: 700;
}

.two-col {
    grid-template-columns: repeat(2, 1fr) !important;
    display: grid;
}

a {
    text-decoration: none;
    color: var(--blue-60) !important;
}

a:hover {
    text-decoration: underline;
}

nav a {
    color: var(--gray-90);
}

.collapsible-trigger {
    display: flex;
    align-items: center;
    cursor: pointer;
}

.collapsible-trigger::before {
    content: url('https://uploads-ssl.webflow.com/624da42b5f2beca5145266dc/624da42b5f2bec5610526dac_select-arrow.svg');
    margin-right: 6px;
    scale: .85;
    transform: rotate(-90deg);
}

.collapsible-trigger.active::before {
    transform: rotate(0deg);
}

#business-impact-of-fivetran .collapsible-trigger::before {
    scale: 1.2;
    margin-right: 12px;
}

.report-table-section, .grand-total {
    grid-column: 1 / span 12;
    grid-row: auto;
}

.report-table-section {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.total-wrapper {
    background: var(--blue-05);
    border: 1px solid var(--blue-60);
    border: 1px solid var(--blue-60) !important;
    padding: 20px !important;
    margin-left: -20px;
    margin-right: -20px;
    margin-top: 24px;
    border-radius: 4px;
}

.report-table-section > div {
    grid-column: 1 / span 12;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 20px;
}

.report h3 {
    grid-column: 1 / span 12;
    margin-bottom: -12px;
}

.report {
    grid-template-columns: repeat(12, 1fr);
    background: white !important;
    border-radius: 0px !important;
    border: 1px solid var(--gray-40);
    padding: 60px !important;
}

.report-heading {
    grid-column: 1 / span 6;
}

.report-heading > p {
    font-size: 14px;
    font-weight: 500;
    margin-bottom: 8px;
}

.report-heading > p:nth-child(2) {
    color: var(--gray-60);
    font-style: italic;
}

.report-heading h2 {
    font-size: 28px !important;
    margin-bottom: 24px !important;
}

.report-subhead {
    margin-top: 4px;
    font-size: 16px;
    line-height: 20px;
}

.report-logo {
    grid-column: 10 / span 3;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: flex-end;
}

.input-group {
    grid-template-columns: subgrid;
    display: grid;
    grid-column: 1 / -1;
    row-gap: 48px;
}

.report-logo img {
    width: 250px;
}

:root {
    --gray-05: #F7F8FA;
    --gray-10: #EDEFF2;
    --gray-40: #B0B2B8;
    --gray-60: #626366;
    --gray-90: #222222;
    --citron-10: #F4FFD3;
    --blue-05: #EBF1FF;
    --blue-60: #306bea;
    --blue-70: #2E60CF;
    --apricot-10: #FFDBC0;
    --red-05: #FFE8E7;
    --red-70: #D51A11;
}

/* resets */
fieldset {
    border: 0;
    padding: 0 0 0 0;
    margin: 0;
    min-width: 0;
    gap: 16px;
}

p {
    margin: 0;
}

body:not(:-moz-handler-blocked) fieldset {
    display: table-cell;
}

input {
    min-width: 0
}

/* end resets */

* {
    font-family: 'Inter', sans-serif;
    box-sizing: border-box;
    color: var(--gray-90);
}

main {
    display: flex !important;
    row-gap: 60px;
    padding-bottom: 60px;
    flex-direction: column;
    align-items: center;
    justify-content: flex-start;
}

form {
    width: 100%;
    max-width: 1320px;
    display: flex;
    align-items: left;
    flex-direction: column;
    gap: 40px;
}

.form-block {
    width: 100%;
    max-width: 1320px;
    display: grid;
    grid-template-columns: repeat(12, 1fr);
    grid-template-rows: auto;
    column-gap: 20px;
    row-gap: 72px;
    padding: 40px;
    background: var(--gray-05);
    border-radius: 8px;
}

h1, h2, h3, h4, h5, h6, legend, label {
    font-weight: 600 !important;
    margin: 0;
}

h1 {
    font-size: 36px !important;
    line-height: 48px !important;
}

h2 {
    font-size: 24px !important;
    line-height: 36px !important;
}

h3 {
    margin-bottom: 16px !important;
}

input, output, .const-input {
    border-radius: 4px;
    border: 1px solid var(--gray-40);
    background: white;
    padding: 6px 4px 6px 12px;
    font-size: 14px;
    font-weight: 400px;
    display: flex;
    align-items: center;
}

.const-input {
    background: var(--gray-05);
}

legend, label, .row-header span {
    font-weight: 600;
    font-size: 14px;
    line-height: 20px;
}

legend {
    width: 100%;
}

label, .label-like {
    font-size: 14px;
    line-height: 20px;
    display: flex !important;
    justify-content: space-between;
    font-weight: 500 !important;
    margin-bottom: 0 !important;
}

header {
    padding-top: 20px;
    padding-bottom: 20px;
    width: 100%;
    display: flex !important;
    justify-content: space-between;
    max-width: 1320px;
}

header img {
    height: 32px;
    width: auto;
    display: block;
}

header ul {
    display: flex;
    list-style: none;
    font-size: 14px;
    gap: 16px;
    margin: 0;
}

.top-nav {
    display: flex;
    justify-content: center;
    margin-bottom: 72px;
}

.row-header {
    border-bottom: 1px solid var(--gray-90) !important;
    padding: 0px 0px 8px 0px;
    margin-bottom: 32px;
    font-weight: 600 !important;
}

.row-header *:nth-child(n+2), .report-table-row *:nth-child(n+2) {
    text-align: right;
}

.report-table-row {
    border-bottom: 1px solid var(--gray-10);
    padding-bottom: 8px;
}

.report-table-row.row-header span {
    font-size: 16px !important;
}

.report-table-row:not(.row-header) > *:first-child {
    font-weight: 500;
}

.report-table-row:not(.row-header) > *:last-child {
    font-weight: 500;
}

/* reset if legend is a child of a table-header style element */

.field-label {
    display: flex;
    flex-direction: column;
    gap: 8px;
    align-items: stretch;
}

.field-box {
    display: flex;
    align-items: center;
    flex-basis: 50%;
    gap: 20px;
    padding: 12px;
    border-radius: 4px;
    background: var(--gray-10);
    border: 1px solid var(--gray-40);
}

.field-box label {
    flex: 2 1 60%;
}

.field-box input, .field-box output {
    flex: 2 1 40%;
}

.annotated-input {
    display: grid;
    gap: 16px;
    grid-template-columns: 2fr 1fr;
    align-items: center;
    justify-items: stretch;
}

.annotated-label {
    display: flex;
    flex-direction: column;
    gap: 8px;
    max-width: 45ch;
}

.annotated-label p {
    font-size: 14px;
    line-height: 16px;
    font-style: italic;
    font-weight: 400;
}

.annotated-input label {
    font-weight: 400;
    font-style: italic;
    text-align: right;
    font-size: 12px;
    line-height: 14px;
    display: unset;
}

label.required::after {
    content: '*required';
    font-style: italic;
    color: var(--red-70);
    font-size: 12px;
    font-weight: 400;
    margin-left: auto;
}

output {
    background: var(--blue-05);
    border: 1px solid var(--blue-60);
    color: var(--blue-70);
    font-weight: 500;
}

#company-profile {
    grid-template-areas:
        'one one one one one one one one one one one one'
        'two two two two blank three three three three three three three'
        'two two two two blank four four four four four four four';
}

#company-profile h2 {
    grid-area: one;
}

#contact-information {
    grid-area: two;
}

#current-staffing-costs {
    grid-area: three;
}

#work-schedule {
    grid-area: four;
}

#data-integration-cost-and-maintenance {
    grid-template-areas: 
    "one one one one one one one one one one one one"
    "two two two two . . . . . . . ."
    "three three three three three three three three three three . ."
    "four four four four four four four four four four . ."
    "five five five five five five five five five five . ."
    "six six six six six six six six six six . ."
    "seven seven seven seven eight eight eight eight . . . ."
}

#data-integration-cost-and-maintenance h2 {
    grid-area: one;
}

#number-of-engineers {
    grid-area: two;
}

#data-integration-cost-and-maintenance > fieldset { 
    display: grid;
    grid-template-columns: subgrid;
}

#data-integration-cost-and-maintenance > fieldset > *, #total-time  {
    grid-column: 1 / span 12;
    display: grid;
    grid-template-columns: 4fr 3fr 3fr;
    gap: 20px;
    align-items: center;
}

#pipelines {
    grid-area: three;
}

#data-integration-cost-and-maintenance .row-header {
    margin-bottom: 0;
}

#transformations {
    grid-area: four;
}

#total-time {
    padding: 12px;
    grid-area: five;
    background: var(--gray-10);
    margin-left: -12px;
    margin-right: -12px;
    border-radius: 4px;
    border: 1px solid var(--gray-40);
    margin-bottom: 20px;
}

#additional-comparisons-and-costs {
    grid-area: six;
}

#cost-of-data-downtime-per-hour {
    grid-area: seven;
}

#additional-costs {
    grid-area: eight;
}

#business-impact-of-fivetran {
    grid-template-columns: repeat(12, 1fr);
}

#business-impact-of-fivetran h2 {
    grid-column:  1 / span 12;
}

#business-impact-of-fivetran hgroup {
    grid-column:  1 / span 8;
}

#business-impact-of-fivetran fieldset {
    grid-column: 1 / span 12;
    display: grid;
    grid-template-columns: subgrid;
}

.input-row {
    align-items: center;
}

#productivity-gains-with-fivetran .row-header, #productivity-gains-with-fivetran .input-row {
    grid-column: 1 / span 12;
    display: grid;
    grid-template-columns: 3fr 2fr 2fr 2fr 2fr 1fr;
    gap: 20px;
}

#overall-revenue-gains-and-operational-efficiency .row-header, #overall-revenue-gains-and-operational-efficiency .input-row {
    grid-column: 1 / span 12;
    display: grid;
    grid-template-columns: 5fr 2fr 2fr 2fr 1fr;
    gap: 20px;
}

input[type=submit], button {
    background: var(--blue-60);
    color: white !important;
    border: none;
    padding: 8px 16px 8px 16px;
    border-radius: 4px;
    font-size: 16px;
    line-height: 20px;
    font-weight: 500;
    cursor: pointer;
    align-self: start;
}

input[type=submit]:hover, button:hover {
    background: var(--blue-70);
}

input[type="checkbox"] {
    accent-color: var(--blue-60);
    justify-self: end;
    scale: 1.5;
}

.invalid,
.invalid:focus {
    outline: red;
    border-color: red;
}

#print-button {
    width: 100%;
    max-width: 1320px;
}

/* utility classes */

.flex-column {
    flex-direction: column;
    display: flex;
    gap: 20px;
}

.flex-row {
    flex-direction: row;
    display: flex;
    gap: 20px;
    align-items: start;
    height: min-content;
}

.subgrid { grid-template-columns: subgrid; }

@media print {

    body {
        -webkit-print-color-adjust: exact !important;
        print-color-adjust: exact !important;
    }

    form {
        display: none;
    }

    .top-nav {
        display: none;
    }

    .form-block.report {
        border: none;
    }
    #print-button {
        display: none;
    }
}

</style>
