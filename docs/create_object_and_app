Create an Object and an App from a spreadsheet Data Model Using Clicks Reference Guide
Salesforce Trailhead: DreamHouse Realty (Unit 2)
What This Covers
Building the House custom object from a spreadsheet, exploring Salesforce's built-in features, creating the Dreamhouse app, retrieving metadata into your local project, and completing the Verify step.


Step-by-Step
1. Prep the Spreadsheet
Download the module's spreadsheet and save it as House.csv.
2. Create the House Custom Object
Setup → Object Manager → Create → Custom Object from Spreadsheet
Login With Salesforce → enter your Playground credentials → Allow
Upload → select House.csv
Record Name field: House Name (leave other mappings as-is) → Next
Enter:
Label: House
Plural Label: Houses
API Name: House (Salesforce appends __c, giving House__c)
Finish

The module text shows "HouseCopy," "HousesCopy," etc. , that's a leftover copy-button artifact. Type just House / Houses.
3. Explore Auto-Generated Features (optional)
App Launcher → Houses → Recently Viewed → All Records (list view)
Open a record → Edit → Save (this is the built-in CRED UI)
All generated automatically — no code involved.
4. Build the Dreamhouse App
Setup → Quick Find "App Manager" → New Lightning App
App Name: Dreamhouse; upload dreamhouse-logo.png → Next
Standard navigation → Next → skip Utility Items → Next
Navigation Items: add Home (house icon), Houses, Reports, Dashboards → Next
User Profiles: add System Administrator → Save & Finish
App Launcher → Dreamhouse to confirm it loads
5. Retrieve House Object Metadata (VS Code)
Activity Bar → Org Browser → Custom Objects → House__c → Retrieve source from org Lands in force-app/main/default/objects.
6. Retrieve Remaining Metadata (CLI)
sf project retrieve start --metadata CustomApplication:Dreamhouse CustomTab:House__c "Layout:House__c-House Layout"
7. Complete the Verify Step
On the Trailhead module page, confirm the correct hands-on org is selected, then click Launch. Trailhead checks your org automatically for +100 points.


Quick Reference
Item
Value
Custom object Label
House
Custom object Plural Label
Houses
Custom object API Name
House__c
Lightning App Name
Dreamhouse
Retrieved metadata location
force-app/main/default/objects
CLI: retrieve app/tab/layout
sf project retrieve start --metadata CustomApplication:Dreamhouse CustomTab:House__c "Layout:House__c-House Layout"
CLI: retrieve object only
sf project retrieve start --metadata CustomObject:House__c



Troubleshooting
"command 'sfdxOrgBrowser.showLocal.on' not found"
Try in order:

Developer: Reload Window (Command Palette)
Confirm VS Code is opened at the project root — the folder containing sfdx-project.json
Extensions panel → update Salesforce Extension Pack (Expanded) → reload
Check for a conflicting install of the plain Salesforce Extension Pack alongside the Expanded one — uninstall the duplicate if present
View → Output → select the "Salesforce CLI"/"Salesforce DX" channel to see the real underlying error
Workaround: skip the button and run:

sf project retrieve start --metadata CustomObject:House__c


