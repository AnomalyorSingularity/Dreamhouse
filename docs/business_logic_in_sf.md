Write Business Logic in Apex Reference Guide
Salesforce Trailhead: DreamHouse Realty (Unit 3)
What This Is For
This unit adds a backend layer to the House data model built in Unit 2. You write an Apex class, HouseService, that queries the House__c custom object via SOQL and exposes the results so a future Lightning web component can display them. It's the bridge between the data model and the UI built in later units.


Step-by-Step
Create the class. In VS Code, right-click classes under force-app/main/default → SFDX: Create Apex Class → name it HouseService.
Paste the code below into the file and save.
Deploy it. Right-click HouseService.cls → SFDX: Deploy Source to Org. Look for a success confirmation — this also compiles it server-side.
Create a test script. New file at scripts/apex/dreamhouseapp.apex (create the apex subfolder under scripts if needed).
Add the test line and run it:

System.debug(HouseService.getRecords());

Click the Execute Code Lens link above the line, or right-click → SFDX: Execute Anonymous Apex with Editor Contents.

Check the Output panel, it opens automatically and shows a debug log listing your House records (Id, Name, Address__c, etc.).
Complete the Verify step on the Trailhead module page: confirm the correct hands-on org is selected, click Launch, +100 points.

Note: the module text shows "HouseServiceCopy", that's a Trailhead copy-button artifact. The actual class name is just HouseService.


The Code, Explained
// "with sharing" enforces the running user's record-level sharing rules --

// this class can't be used to bypass sharing settings on House__c records.

public with sharing class HouseService {

    // @AuraEnabled exposes this method to Lightning web/Aura components.

    // cacheable=true marks it as read-only, so the LWC framework can cache

    // results client-side instead of re-querying the server every time.

    @AuraEnabled(cacheable=true)

    public static List<House__c> getRecords() {

        try {

            // SOQL embedded directly in Apex. Because House__c and its fields

            // already exist in the org, this query is type-checked at compile

            // time -- a typo like "Adress__c" fails to deploy, not at runtime.

            List<House__c> lstHouses = [

                SELECT

                   Id,            // Standard record ID

                   Name,          // The "House Name" field mapped in Unit 2

                   Address__c,

                   State__c,

                   City__c,

                   Zip__c

                   FROM House__c

                   // Runs the query under the current user's object/field-level

                   // security and sharing rules, layered on top of "with sharing."

                   WITH USER_MODE

                   ORDER BY CreatedDate  // Oldest houses first

                   LIMIT 10   // Governor-limit-friendly cap on rows returned

                ];

            return lstHouses;

        }

        // Any error here (e.g. a security exception from WITH USER_MODE) is

        // re-thrown as AuraHandledException -- the only exception type whose

        // message is safely visible to client-side JavaScript/LWC code.

        catch (Exception e) {

           throw new AuraHandledException(e.getMessage());

        }

    }

}



Quick Reference
Item
Value
Class name
HouseService
Method
getRecords()
Object queried
House__c
Test script path
scripts/apex/dreamhouseapp.apex
Anonymous Apex test line
System.debug(HouseService.getRecords());



Key Concepts
with sharing = enforces the running user's sharing rules on this class.
WITH USER_MODE = runs the SOQL query under the current user's field/object-level security, independent of the class's own access level.
@AuraEnabled(cacheable=true) = exposes a method to LWC/Aura and allows client-side caching; only valid for read-only methods.
AuraHandledException = the only exception type whose message reaches LWC JavaScript; always wrap other caught exceptions in it before re-throwing.
Anonymous Apex = a one-off .apex script that compiles and runs immediately without being saved as org metadata, useful for quick tests.


Troubleshooting
Deploy fails: check that the field API names in the query exactly match the House object (Object Manager → House → Fields & Relationships). A mismatch is a compile-time error, not a runtime one.
No "Execute" Code Lens appears: confirm the file has a .apex extension and lives inside scripts/apex/.
"command 'sfdxOrgBrowser.showLocal.on' not found" or other SFDX commands missing: reload the VS Code window, confirm the workspace is opened at the project root (contains sfdx-project.json), and check for a duplicate/conflicting Salesforce extension install.


