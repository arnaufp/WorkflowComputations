### Workflow: workflows_yottaAFLJToOutstanding_624be815150b340153ec87a1
### Project: customers_devonCountyCouncilTest_6005c6953994fa0064c0e71a
<br><br>
![mySVGFile (20)](https://user-images.githubusercontent.com/7857485/172356415-984d4a7c-577a-4529-ab76-1ba935297daa.svg)

Overview:
When LJ (Super JOb) changes to 'Outstanding' status:
- Job Work Items of the LJ (Task Orders) are copied to the Super Job
- Geometry of the Super Job is updated by merging all the geometries from the Task Orders
- Sets Super Job 'Budget Code' and 'Priority' attribute based on the value of the 'Task' attribute
- Sets 'Budget Code', 'Priority' and 'Status' of all the Task Orders (same as Super Job)
- Sets 'Team' of the Task Order based on location
- If Estimated Costs are set and are bigger than 0 it creates a Purchase Order and PO Line items  and sends it to Finest for approval
- For Single Jobs it only does the Purchase Order and Finest bit above

### Actions


>### 624be815150b340153ec87a0
> Trigger
<br>
<br>

>### 624be8ac4ebcde015d5fcf10
> designs_workflowFilterAction  
> ancestorId: [624be815150b340153ec87a0](#624be815150b340153ec87a0)  
> description: Regular Filter: Job Type = Super Job & Status = Outstanding

<br>
<br>

>### 624be8ce4ebcde015d5fd018
> designs_workflowFilterAction  
> ancestorId: [624be8ac4ebcde015d5fcf10](#624be8ac4ebcde015d5fcf10)  
> description: Regular Filter: if Super Job is connected to JWIs follow this branch

<br>
<br>

>### 624beafaa927080158779db5
> designs_workflowRelationAction  
> ancestorId: [624be8ce4ebcde015d5fd018](#624be8ce4ebcde015d5fd018)  
> description: Regular Relation: gets the JWIs of the Super Job

<br>
<br>

>### 624beb1e150b340153ecc0c0
> designs_workflowDeleteItemAction  
> ancestorId: [624beafaa927080158779db5](#624beafaa927080158779db5)  
> description: Regular Delete: delete all JWIs of the Super Job

<br>
<br>

>### 624beb4a4e22d3015b27fc90
> designs_workflowOutputAction  
> ancestorId: [624beb1e150b340153ecc0c0](#624beb1e150b340153ecc0c0)  
> description: Regular Output: Outputs the Super Job

<br>
<br>

>### 624beb854ebcde015d5ff765
> designs_workflowFilterAction  
> ancestorId: [624beb4a4e22d3015b27fc90](#624beb4a4e22d3015b27fc90)  
> description: Regular Filter: Check if Super Job is linked to a Project

<br>
<br>

>### 624bebac4ebcde015d5ff899
> designs_workflowRelationAction  
> ancestorId: [624beb854ebcde015d5ff765](#624beb854ebcde015d5ff765)  
> description: Regular Relation: Super Job to Project to Lighting Jobs (tasks)

<br>
<br>

>### 624bebc04e22d3015b2801e1
> designs_workflowFilterAction  
> ancestorId: [624bebac4ebcde015d5ff899](#624bebac4ebcde015d5ff899)  
> description: Regular Filter: get the LJ Task Orders

<br>
<br>

>### 624bec74150b340153ecd515
> designs_workflowRelationAction  
> ancestorId: [624bebc04e22d3015b2801e1](#624bebc04e22d3015b2801e1)  
> description: Regular Relation: Task Orders To JWIs

<br>
<br>

>### 624becd361fae7015a3dd4e9
> designs_workflowCreateItemAction  
> ancestorId: [624bec74150b340153ecd515](#624bec74150b340153ecd515)  
> description: Regular Create: creates as many JWIs as it gets as input. All link to Super Job (Parent) 

<br>
<br>

>### 624c30f04e22d3015b2cc04a
> designs_workflowOutputAction  
> ancestorId: [624becd361fae7015a3dd4e9](#624becd361fae7015a3dd4e9)  
> description: Regular Output: outputs the Super Job

<br>
<br>

>### 624c311c150b340153f173f4
> designs_workflowEditItemAction  
> ancestorId: [624c30f04e22d3015b2cc04a](#624c30f04e22d3015b2cc04a)  
> description: Computed Edit: gets all Task Orders geometries and merge them into a Geometry Collection feature

```json
{
	"actionDesignCode": "designs_workflowEditItemAction",
	"ancestorId": "624c30f04e22d3015b2cc04a",
	"signature": "6284befa5854c4016f4d38d6",
	"description": "",
	"parameters": [
		{
			"attributeCode": "attributes_itemsGeometry",
			"value": {
				"script": "return geometryCollection;",
				"discriminator": "WorkflowSyntaxNodeScriptWebModel"
			},
			"discriminator": "WorkflowComputedItemAttributeWebModel"
		}
	],
	"variables": [
		{
			"name": "geometries",
			"value": {
				"outputAction": "624bebc04e22d3015b2801e1",
				"itemValue": {
					"attributeCode": "attributes_itemsGeometry",
					"discriminator": "WorkflowSyntaxArgumentItemValueAttributeWebModel"
				},
				"discriminator": "WorkflowSyntaxNodeOutputWebModel"
			}
		},
		{
			"name": "geometryCollection",
			"value": {
				"script": "return GeometryCollection(Variables.geometries.AllValues.Values.Select(x => x.SingleValue).ToArray());",
				"discriminator": "WorkflowSyntaxNodeScriptWebModel"
			}
		}
	]
}
```
<br>
<br>

>### 624c31ad4e22d3015b2ccfb8
> designs_workflowEditItemAction  
> ancestorId: [624c311c150b340153f173f4](#624c311c150b340153f173f4)  
> description: Regular Edit: change color and icon of Super Job

<br>
<br>

>### 624c41f9a9270801587d59c9
> designs_workflowOutputAction  
> ancestorId: [624be8ce4ebcde015d5fd018](#624be8ce4ebcde015d5fd018)  
> description: Output the Super Job from 624be8ce4ebcde015d5fd018 (alst node of branch above)

<br>
<br>

>### 624c42884e22d3015b2dd94d
> designs_workflowRelationAction  
> ancestorId: [624c41f9a9270801587d59c9](#624c41f9a9270801587d59c9)  
> description: Regular Relation: LJ > Fault Type > Task Priority

<br>
<br>

>### 624c43dd4e22d3015b2de784
> designs_workflowRelationAction  
> ancestorId: [624c41f9a9270801587d59c9](#624c41f9a9270801587d59c9)  
> description: Regular Relation: LJ > Projects > LJ

<br>
<br>

>### 6284a362171225016f54179b
> designs_workflowFilterAction  
> ancestorId: [624c43dd4e22d3015b2de784](#624c43dd4e22d3015b2de784)  
> description: Regular Filter: get the LJ Task Orders

<br>
<br>

>### 6284a5545854c4016f4990c8
> designs_workflowFilterAction  
> ancestorId: [6284a362171225016f54179b](#6284a362171225016f54179b)  
> description: Regular Filter: filter LJ by area

<br>
<br>

>### 6284ad909581780168891210
> designs_workflowEditItemAction  
> ancestorId: [6284a5545854c4016f4990c8](#6284a5545854c4016f4990c8)  
> description: For all Task Orders set same Budget Code, status and priority as the Super Job. Set team based on location

<br>
<br>

>### 6284a5a2171225016f54378e
> designs_workflowFilterAction  
> ancestorId: [6284a362171225016f54179b](#6284a362171225016f54179b)  
> description: Regular Filter: filter LJ by area

<br>
<br>

>### 6284bb4a5854c4016f4ca7b0
> designs_workflowEditItemAction  
> ancestorId: [6284a5a2171225016f54378e](#6284a5a2171225016f54378e)  
> description: For all Task Orders set same Budget Code, status and priority as the Super Job. Set team based on location

<br>
<br>

>### 6284a5bf5854c4016f499ba9
> designs_workflowFilterAction  
> ancestorId: [6284a362171225016f54179b](#6284a362171225016f54179b)  
> description: Regular Filter: filter LJ by area

<br>
<br>

>### 6284bb8d95817801688b05fc
> designs_workflowEditItemAction  
> ancestorId: [6284a5bf5854c4016f499ba9](#6284a5bf5854c4016f499ba9)  
> description: For all Task Orders set same Budget Code, status and priority as the Super Job. Set team based on location

<br>
<br>

>### 6284a6fc5854c4016f49b6cb
> designs_workflowEditItemAction  
> ancestorId: [624c41f9a9270801587d59c9](#624c41f9a9270801587d59c9)  
> description: Set Budget Code and priority of the Super Job based on Fault Type

<br>
<br>

>### 624c4512150b340153f2a7aa
> designs_workflowOutputAction  
> ancestorId: [624be8ce4ebcde015d5fd018](#624be8ce4ebcde015d5fd018)  
> description: Regular Output: outputs the Super Job from branch above (6284a6fc5854c4016f49b6cb)

<br>
<br>

>### 624c489e150b340153f2cb10
> designs_workflowFilterAction  
> ancestorId: [624c4512150b340153f2a7aa](#624c4512150b340153f2a7aa)  
> description: Regular Filter: checks whether the JWIs of the Super Job have estimated costs bigger than 0

<br>
<br>

>### 624c48d961fae7015a43ba9e
> designs_workflowCreateItemAction  
> ancestorId: [624c489e150b340153f2cb10](#624c489e150b340153f2cb10)  
> description: Regular Create: creates a PO with FY coming from 624c45fb61fae7015a43993f

<br>
<br>

>### 624c49f74ebcde015d66340b
> designs_workflowCreateItemAction  
> ancestorId: [624c48d961fae7015a43ba9e](#624c48d961fae7015a43ba9e)  
> description: Computed Create: Create PO Line Item with General Ledger Code info (624c496061fae7015a43c173), ShortDescription =  Job Number and Amount = sum of JWIs estimated costs

<br>
<br>

>### 624c517a61fae7015a442210
> designs_workflowRelationAction  
> ancestorId: [624c49f74ebcde015d66340b](#624c49f74ebcde015d66340b)  
> description: Regular Relation: PO Line Item > PO

<br>
<br>

>### 624c51ac4e22d3015b2e846f
> designs_workflowCallMeshAction  
> ancestorId: [624c517a61fae7015a442210](#624c517a61fae7015a442210)  
> description: Regular Call Mesh

<br>
<br>

>### 624c494461fae7015a43bf68
> designs_workflowRelationAction  
> ancestorId: [624c489e150b340153f2cb10](#624c489e150b340153f2cb10)  
> description: Regular Relation: LJ Super Job > JWIs

<br>
<br>

>### 624c496061fae7015a43c173
> designs_workflowRelationAction  
> ancestorId: [624c489e150b340153f2cb10](#624c489e150b340153f2cb10)  
> description: Regular Relation: LJ > Budget Code > General Ledger Code

<br>
<br>

>### 624beabf4e22d3015b27f3a0
> designs_workflowFilterAction  
> ancestorId: [624be8ac4ebcde015d5fcf10](#624be8ac4ebcde015d5fcf10)  
> description: The branch starting with this node does exactly same things as the branch above. Only difference is that initially SJ does not have JWIs, thus there is no delete node

<br>
<br>


>### 624c45fb61fae7015a43993f
> designs_workflowOutputAction  
> ancestorId: [624be815150b340153ec87a0](#624be815150b340153ec87a0)  
> description: Computed Output: computes the current financial at runtime, formats it to Finest expected format and use that string in a query to get the correct Finest FY item

```json
{
	"actionDesignCode": "designs_workflowOutputAction",
	"ancestorId": "624be815150b340153ec87a0",
	"signature": "6284befa5854c4016f4d38d6",
	"description": "",
	"parameters": [
		{
			"attributeCode": "attributes_workflowOutputActionItems",
			"value": {
				"script": "return fy;",
				"returnOptions": {
					"code": "designs_finestFinancialYears",
					"weakReference": false,
					"defaultValue": [],
					"discriminator": "DodiAttributeOptionsLinkWebModel"
				},
				"discriminator": "WorkflowSyntaxNodeScriptWebModel"
			},
			"discriminator": "WorkflowComputedItemAttributeWebModel"
		}
	],
	"variables": [
		{
			"name": "current_financial_year",
			"value": {
				"script": "var current_UTC_datetime=Now; var current_month = current_UTC_datetime.Month; var current_year = current_UTC_datetime.Year; int first_fy=0; if (current_month>=1 && current_month<=3){first_fy = current_year-1;} else{first_fy = current_year;} var first_fy_string = first_fy.ToString().Substring(first_fy.ToString().Length-2); var second_fy_string=(first_fy+1).ToString().Substring((first_fy+1).ToString().Length-1); var complete_fy_string=first_fy_string+\"/\"+second_fy_string;return complete_fy_string;",
				"discriminator": "WorkflowSyntaxNodeScriptWebModel"
			}
		},
		{
			"name": "fy",
			"value": {
				"aqs": {
					"type": "Query",
					"properties": {
						"attributes": [],
						"collectionCode": [
							"Live"
						],
						"dodiCode": "designs_finestFinancialYears",
						"parameters": [
							{
								"name": "current_financial_year",
								"type": "String"
							}
						]
					},
					"children": [
						{
							"type": "Equals",
							"children": [
								{
									"type": "Attribute",
									"properties": {
										"attributeCode": "attributes_finestFinancialYearsDescription"
									}
								},
								{
									"type": "String",
									"properties": {
										"parameterName": "current_financial_year"
									}
								}
							]
						}
					]
				},
				"discriminator": "WorkflowSyntaxNodeAqsWebModel"
			}
		}
	]
}
```
<br>
<br>

>### 624c59284ebcde015d66cfe0
> designs_workflowFilterAction  
> ancestorId: [624be815150b340153ec87a0](#624be815150b340153ec87a0)  
> description: The branch starting with this node does exactly same things as the super job branches above, but for Single Jobs

<br>
<br>
