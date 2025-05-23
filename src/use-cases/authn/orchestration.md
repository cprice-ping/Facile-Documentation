---
layout: layouts/facile.njk
title: AuthN - Orchestration
eleventyNavigation:
  key: Orchestration
  parent: Authentication
  order: 6
---

OOTB PingFed HTML page with embedded SK Widget.

* [Orchestration](.) --> Policy Contract (No LIP) --> Decoder

Adapter Features:
* SK Details (`CompanyID` \ `FlowID` \ `API Key` \ `SK URL`)
* Flow data returned in a JSON Success with `additionalProperties`
  * Extend the Contact with the fields you want to come out of the Adapter
  * Use OGNL to extract the individual values from `additionalProperties`
  
```ognl
#obj=new org.json.simple.parser.JSONParser().parse(#this.additionalProperties),
#obj.username
```

### SingularKey Flows

This IK shows how to integrate PF with SingularKey

#### Sample Flow

As a demonstration, Facile invokes a Widget that simulates the [Simple](../simple) HTML Form.
The widget launches a Custom HTML Form from SK and validates the password using the PF AuthN API (also in SK), 
with the results of the SK flow delivering data in the `additionalProperties` claim of the Success response.

The UX Flow is `CP - Facile - HTML Form`

![Sample Flow](https://cdn.glitch.me/6f32d434-43ae-4e29-b7fe-c327613b6a03%2FSingularKeyFlow%202.png?v=1637295260902#flow)

#### General Flows

You can point the IK to any flow -- the Widget will run it as part of a PF token request.
Place the data that you want PF to have access to in the `additionalProperties` fields of a JSON Success step
at the end of your Flow.

Extend the Adapter Contract with the values you placed in `additionalProperties` and use OGNL to extract the
individual values (see above).

#### Multiple Flows

You can use the IK to trigger multiple Flows - just define a new IK for each `flowId` and place the Adapter
appropriately into a PF Policy.

