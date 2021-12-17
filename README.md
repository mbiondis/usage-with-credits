# Usage with Credits

## Create the Package
Once the source has been tested, we can turn it into a package.

- Create the Package container
```
sfdx force:package:create -n <package name> -d <description> -t <Unlocked,Managed> -r force-app -e -v <dev hub alias>
```
> This command only edits the `sfdx-project.json` file by adding the package details and its alias
```json
"package": <package name>,
"versionName": "ver 0.1",
"versionNumber": "0.1.0.NEXT"

"packageAliases": {
  <package name>: <package alias>
}
```

- Create the Package version
```
sfdx force:package:version:create -p <package name> -d force-app -x -w 60 -v <dev hub alias>
```

## Install and Test

- Install the package
```
sfdx force:package:install -p "Usage with Credits@1.0.0-2" -u <scratch org alias> -r -w 30 -b 10
```
- Load the test data
```
sfdx sfdmu:run -s csvfile -u <scratch org alias> -p ./data
```

If you've added a **Consumption Schedule**, you'll need to:
- Open `data/ConsumptionSchedule.csv` in Excel
- Change the `IsActive` column to `TRUE`
- Run `sfdx sfdmu:run -s csvfile -u <scratch org alias> -p ./data`

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
- For the `Product2` object
  - Usage Term
  - Overage Surcharge
  - Carryover Factor
  - Carryover Limit


