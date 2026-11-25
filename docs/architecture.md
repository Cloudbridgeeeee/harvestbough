# HarvestBough — proposed AWS architecture

HarvestBough uses AWS to collect estimates from the field, forecast the season and share plans with every partner — reliably, even at harvest peak.

## Request flow

1. Field estimates
2. API Gateway
3. AWS Lambda
4. Amazon S3
5. SageMaker AI
6. DynamoDB
7. Planner approval

## Services

### Amazon SageMaker AI

**Role:** Forecast collection volumes

Trains models that calibrate farm production estimates against past collections, weather and crop calendars to forecast weekly ready-to-collect volumes.

### Amazon API Gateway

**Role:** Connect field and partners

Provides secure APIs for field officer apps, buyer systems and SMS tools to submit estimates and receive approved collection windows.

### Amazon S3

**Role:** Store estimates and season history

Keeps estimate submissions, purchasing schedules and historical collections encrypted as the training history for each season.

### Amazon DynamoDB

**Role:** Serve farms, forecasts and plans

Stores farm groups, forecasts, capacity plans and approved windows with fast reads during the busiest weeks of harvest.

### AWS Lambda

**Role:** Recalculate plans

Validates new submissions and recalculates capacity and collection plans whenever estimates or schedules change.

## Principles

- **Built for harvest peaks** — Serverless services scale with the season.
- **Farmers’ data respected** — Farm data is shared only with partners they work with.
- **Calibrated, not copied** — Estimates are checked against what really happened.

## Safeguards

- **Planners approve** — Collection windows and shipments are proposals until a planner approves them.
- **Honest uncertainty** — Every forecast shows its range, especially early in the season.
- **Fair to farmers** — Forecasts plan logistics; they are not used to set farm-gate prices.
- **Data sharing controls** — Farm data is shared only with partners the cooperative approves.

## MVP scope

For one crop and region, we import farm production estimates and purchasing schedules, forecast weekly collection volumes and capacity needs, and review the plan with your team each week of the season.

- Production estimate import
- Purchasing schedule import
- Weekly collection forecasts
- Truck and storage needs
- End-of-season accuracy report
