---
uid: BIF_RecipeDefaultProperties
---

# Recipe templates defaults

<!-- Topic requires customization for specific interface -->

The following section lists the default recipe template settings for the batch and unit batch levels for Emerson DeltaV. 

## Batch Level
The following are the recipe template default values for the BATCH level:

| Template | Default
| ----- | ----- |
| Name | [Procedure] 
| Value | [BatchID]
| Product | [pval] |
| Product Trigger | [Event,value=\"Recipe Header\"][descript,value=\"Product Code\"]) |
| Category | OSIBatch |
| Template | Procedure |

**Default Properties**

[RECIPE] = 1

      .NAME = Recipe
      .VALUE = [PROCEDURE|UNITPROCEDURE|OPERATION|Phase|PhaseState|PhaseStep]

[PRODUCT] = 2

      .NAME = Product
      .VALUE = [pval]
      .TRIGGER = [Event,value=\"Recipe Header\"][descript,value=\"Product Code\"]

## Unit Batch Level
The following are the recipe template default values for the UNIT BATCH level:

| Template | Default
| ----- | ----- |
| Name | [UnitProcedure] 
| Value | [BatchID]
| Product | [pval] |
| Product Trigger | [Event,value=\"Recipe Header\"][descript,value=\"Product Code\"]) |
| SearchByStartTime = true | 
| SearchByEndTime = true |
| Category | OSIBatch |
| Template | UnitProcedure |
| Module Path | [AREA]\\[PROCESSCELL]\\[UNIT])

**Note** - When SearchByStartTime and SearchByEndTime equal true, we assume that there can be unitbatches with the same name.

**Default Properties**

[PROCEDURE] = 3

      .NAME = PROCEDURE
      .VALUE = [UNITPROCEDURE|OPERATION|Phase|PhaseState|PhaseStep]

[PRODUCT] = 2

      .NAME = Product
      .VALUE = [pval]
      .TRIGGER = [Event,value=\"Recipe Header\"][descript,value=\"Product Code\"]

[RECIPE] = 1

      .NAME = BatchID
      .VALUE = BatchID

## Operation Level
The following are the recipe template default values for the OPERATION level:

| Template | Default
| ----- | ----- |
| Name | [Operation] 
| Category | OSIBatch |
| Template | UnitProcedure |

## Phase Level
The following are the recipe template default values for the PHASE level:

| Template | Default
| ----- | ----- |
| Name | [Phase] 
| Category | OSIBatch |
| Template | Phase |
| Module Path | [AREA]\\[PROCESSCELL]\\[UNIT]\\[PHASEMODULE])

## Phase State Level
The following are the recipe template default values for the PHASE STATE level:

| Template | Default
| ----- | ----- |
| Name | [PhaseState] 
| SearchDirection | Reverse |
| SearchByStartTime = true | 
| SearchByEndTime = true |
| Category | OSIBatch |
| Template | PhaseState |

## Phase Step Level
The following are the recipe template default values for the PHASE STEP level:

| Template | Default
| ----- | ----- |
| Name | [PhaseStep] |
| Merge | false |
| SearchDirection | Reverse // search in Reverse (default: always FORWARD) |
| Category | OSIBatch |
| Template | PhaseState |
