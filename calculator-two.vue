<script>
//default value appears to be unecessary when using v-model
export default {
    data() {
        const defaults = {
            averageSalary: 80000,
        }
        return {
            //company profile
            //contact information
            companyName: {
                required: true,
                value: ''
            },

            prospectiveCustomerEmail: {
                required: true,
                value: ''
            },

            fivetranContactEmail: {
                required: true,
                value: ''
            },

            //current staffing costs
            averageSalary: {
                required: true,
                value: defaults.averageSalary,
                increment: 1000,
                annotation: 'thousands, $'
            },

            //work schedule
            hoursWorkedPerWeek: {
                required: true,
                value: 40
            },

            weeksWorkedPerYear: {
                required: true,
                value: 48
            },

            //data integration cost and maintenance

            numberOfEngineers: {
                required: true,
                value: 1,
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
                annotation: 'annual, $',
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
                    increment: .1
                },
                withFivetran: {
                    default: 99.99,
                    annotation: 'Reduced downtime with Fivetran',
                    increment: .1
                }
            },
            destinationIngestionCosts: {
                annotation: 'annual, $',
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
                annotation: 'annual, $',
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
                increment: 1000
            },

            //productivity gains by function section
            idcWorkFunctions: {
                dataEngineers: {
                    customSalarySet: { value: false },
                    equivalentProductivityLevel: { value: 0 },
                    salary: { value: 70000 },
                    productivityGain: { value: 0.48 },
                    include: { value: false },
                },
                dataAnalytics: {
                    customSalarySet: { value: false },
                    equivalentProductivityLevel: { value: 0 },
                    salary: { value: 70000 },
                    productivityGain: { value: 0.02 },
                    include: { value: false },
                },
                dataGovernance: {
                    customSalarySet: { value: false },
                    equivalentProductivityLevel: { value: 0 },
                    salary: { value: 70000 },
                    productivityGain: { value: 0.16 },
                    include: { value: false },
                },
                finance: {
                    customSalarySet: { value: false },
                    equivalentProductivityLevel: { value: 0 },
                    salary: { value: 70000 },
                    productivityGain: { value: 0.40 },
                    include: { value: false },
                },
                productManagement: {
                    customSalarySet: { value: false },
                    equivalentProductivityLevel: { value: 0 },
                    salary: { value: 70000 },
                    productivityGain: { value: 0.12 },
                    include: { value: false },
                },
                salesAndCustomerSuccess: {
                    customSalarySet: { value: false },
                    equivalentProductivityLevel: { value: 0 },
                    salary: { value: 70000 },
                    productivityGain: { value: 0.19 },
                    include: { value: false },
                },
                logistics: {
                    customSalarySet: { value: false },
                    equivalentProductivityLevel: { value: 0 },
                    salary: { value: 70000 },
                    productivityGain: { value: 0.29 },
                    include: { value: false },
                },
                marketing: {
                    customSalarySet: { value: false },
                    equivalentProductivityLevel: { value: 0 },
                    salary: { value: 70000 },
                    productivityGain: { value: 0.16 },
                    include: { value: false },
                }
            },

            //Overall revenue gains and operational efficiency section
            revenueGains: {
                customSalarySet: { value: false },
                additionalGrossRevenue: { value: 554894 },
                margin: { value: .15 },
                include: { value: false },
            },

            operationalCostSavings: {
                customSalarySet: { value: false },
                oneTime: { value: 285714 },
                annual: { value: 177400 },
                include: { value: false },
            }
        }
    },
    computed: {
        
        //calculates an hourly rate based on average salary and work schedule inputs in staffing costs section
        equivalentHourlyRate() {
            return this.averageSalary.value / (this.weeksWorkedPerYear.value * this.hoursWorkedPerWeek.value)
        },
        //displayed beneath pipelines/transformations inputs
        //sums hours in before and after Fivetran scenarios for both categories
        totalTime() {
            let pipelines = Object.values(this.pipelines);
            let transformations = Object.values(this.transformations);

            console.log(pipelines)

            let totalCurrentPipelineHours = pipelines.reduce((total, obj) => obj.currentState.value + total, 0);
            let totalFivetranPipelineHours = pipelines.reduce((total, obj) => obj.withFivetran.value + total, 0);

            let totalCurrentTransformationsHours = transformations.reduce((total, obj) => obj.currentState.value + total, 0);
            let totalFivetranTransformationsHours = transformations.reduce((total, obj) => obj.withFivetran.value + total, 0);

            console.log(totalCurrentPipelineHours)

            let currentState = totalCurrentPipelineHours + totalCurrentTransformationsHours;
            let withFivetran = totalFivetranPipelineHours + totalFivetranTransformationsHours;

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
                if (this.idcWorkFunctions[key].equivalentProductivityLevel.value > 0) {
                    idcProductivityGains[key] = this.calculateIDCGains(this.idcWorkFunctions[key].salary.value, this.idcWorkFunctions[key].equivalentProductivityLevel.value, this.idcWorkFunctions[key].productivityGain.value)
                }
            }
            return idcProductivityGains;
        },

        //associated with Revenue Gains line, second-to-last IDC input
        annualNetGain() {
            return this.revenueGains.additionalGrossRevenue.value * this.revenueGains.margin.value;
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
            let averageAnnualGain = this.calculateCostSavings(withFivetran, currentState);
            return {
                currentState: currentState,
                withFivetran: withFivetran,
                averageAnnualGain: averageAnnualGain
            }
        },
        calculateCostSavings(withFivetran, currentState) {
            return withFivetran - currentState;
        },
        updateIDC() {
            for(idcWorkFunctions of idcWorkFunctions) {
                if (!idcWorkFunction.customSalarySet) {
                    this.idcWorkFunction.salary.value = this.averageSalary;
                }
            }
        }
    },
}

</script>
