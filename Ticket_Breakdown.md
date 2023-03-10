# Ticket Breakdown
## Ticket 1
**Allow a facility to generate custom ids for each agents**

As a facility manager, I should be able to run a function, which lets me create a custom ID for an agent working in my facility

As a developer, I want to create a function `generateAgentIdForFacility(facilityId: number|string, agentId: number|string, customId: string)`. Also, I need to create a new table which will associate a facility with an agent and the custom Id for that agent. A pivot table name `Facility_Agent` with the following schema can be used:
```ts
Facility_Agent {
    facilityId: number|string;
    agentId: number|string;
    customId: string;
}
```
When this function is run, it should create a new record in the table using the parameters supplied to the function.

### Effort required
Medium

### Time estimate
2 hours

### Acceptance criteria
- Once the function to generate the custom id is run, the custom id shows up in the database table
- There are no duplicate records of the facility and the agent


## Ticket 2
**Refactor the getShiftsByFacility(facilityId) function**

As a developer, I want to refactor the `getShiftsByFacility(facilityId: number|string)` function such that the metadata of the agent that is returned with each shift optionally contains their custom id for that facility to be used in generating the report. Each returned `Shift` object should look like this:
```ts
Shift {
    // ...shift data
    agent: {
        // ...previous metadata
        customId?: string; // the custom ID of the agent for that facility
    }
}
```

### Effort required
Simple

### Time estimate
30 minutes

### Acceptance criteria
- Running this function against a shift with an agent that has a custom id generated by the facility should return the custom id of the agent as part of the agent metadata for that shift


## Ticket 3
**Refactor the generateReport(Shift[]) function**

As a developer, I want to refactor the `generateReport(Shift[])` function such that it puts into consideration the optional customId of the agent for a shift. Use a ternary operator to determine which id to use on the report - if the customId of the agent exists, use that, otherwise, the internal database id would suffice (this is for facilities that are yet/decide not to create a custom id for the agent).

### Effort required
Simple

### Time estimate
30 minutes

### Acceptance criteria
- Running this function against a shift with an agent that has a custom id generated by the facility should display the custom id of the agent on the PDF report generated for the shift for compliance.
- For backward compatibility, ensure that if a custom ID is not generated for an agent yet, the internal database id should be displayed on the PDF
