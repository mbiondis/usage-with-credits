## Install and Test

- Install the package
```
sfdx force:package:install -p "Usage with Credits@1.0.0-2" -u <scratch org alias> -r -w 30 -b 10
```
- Load the test data
```
sfdx sfdmu:run -s csvfile -u <scratch org alias> -p ./data
```

Because there's a **Consumption Schedule** in the test data:
- Open `data/ConsumptionSchedule.csv` in Excel
- Change the `IsActive` column to `TRUE`
- Run
```
sfdx sfdmu:run -s csvfile -u <scratch org alias> -p ./data
```

> **Explanation** \
The Consumption Schedules are inserted into an org as inactive because otherwise the Consumption Rates cannot be added due to a validation rule. \
Conversely, there's another validation that prevents linking a Product with a Consumption Schedule that's inactive.

## Add the Picklist values
- Go to **Setup > Objects and Fields > Picklist Value Sets**
- Search for `Unit of Measure` and click on it
- Under **Values**, click `New`
- Add the following values
  - `Amount`
  - `Transaction`
- Go to **Setup > Object Manager**
- Click on `Consumption Schedule`
- Click on `Unit of Measure`
- Under **Inactive Values**, `Activate` both values

## Add the relevant fields to page layouts
- For the **Product2** object
  - `Usage Term`
  - `Overage Surcharge`
  - `Carryover Factor`
  - `Carryover Limit`

