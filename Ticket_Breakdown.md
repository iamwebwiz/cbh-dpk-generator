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
