Build a Reusable UI Component with Lightning Web Components Reference Guide
Salesforce Trailhead: DreamHouse Realty (Unit 4 Final Unit)
What This Is For
This unit builds the front end that displays the House data on a map. You create a Lightning web component, housingMap, that wires to the HouseService.getRecords() Apex method (built in Unit 3) and renders the results using Salesforce's built-in lightning-map base component. This is the piece that finally makes the data model and backend logic visible to a user.


Step-by-Step
Create the LWC. Right-click the lwc folder under force-app/main/default → SFDX: Create Lightning Web Component → name it housingMap, type: JavaScript.
Add the HTML (below) to housingMap.html, save.
Add the JavaScript (below) to housingMap.js, save.
Update the metadata XML (below) in housingMap.js-meta.xml, save.
Deploy. Right-click anywhere in the housingMap folder → SFDX: Deploy This Source to Org.
Open your org. Command Palette → SFDX: Open Default Org → App Launcher → Dreamhouse → Home tab.
Add the component to the Home page. Gear icon → Edit Page → drag housingMap from the custom components list to the top of the canvas → Save → Activate → Assign as Org Default → Save → Save again → Back → refresh to see the map.
Complete the Verify step on the Trailhead module page. This is the final unit — completing it finishes the whole project.


The Code, Explained
housingMap.html

<template>

  <!-- lightning-card provides standard Salesforce card chrome (header, border, padding) for free -->

  <lightning-card title="Housing Map">

    <!-- Base component from Salesforce's component library — handles the Google Maps

         integration internally, so no custom markup or JS is needed for the map itself.

         map-markers={mapMarkers} binds this attribute to the mapMarkers property

         defined in the JS controller below; {} is LWC's data-binding syntax. -->

    <lightning-map map-markers={mapMarkers}> </lightning-map>

  </lightning-card>

</template>

housingMap.js

// LightningElement is the base class every LWC extends.

// wire is the decorator used to declaratively bind data (from Apex, in this case) to the component.

import { LightningElement, wire } from "lwc";

// Imports the getRecords() Apex method from HouseService as a callable JS function.

// This import path only works because the method is marked @AuraEnabled in Apex.

import getHouses from "@salesforce/apex/HouseService.getRecords";

export default class HousingMap extends LightningElement {

    mapMarkers; // Holds the array of markers, formatted for lightning-map

    error;      // Holds any error the wire service reports

    // @wire calls getHouses() automatically when the component loads (and again if

    // its underlying data changes) no manual fetch/subscribe code required.

    // The destructured { error, data } is how the wire service reports its result.

    @wire(getHouses)

    wiredHouses({ error, data }) {

        if (data) {

            // lightning-map expects an array shaped like { location: {...}, title: "..." }.

            // Array.map() transforms each House__c record from Apex into that shape.

            this.mapMarkers = data.map((element) => {

                return {

                    location: {

                        Street: element.Address__c,

                        City: element.City__c,

                        State: element.State__c

                    },

                    title: element.Name

                };

            });

            this.error = undefined; // Clear any previous error once data arrives

        } else if (error) {

            // If the wire service reports an error instead of data, capture it and

            // clear stale markers so a bad map isn't shown alongside the error.

            this.error = error;

            this.mapMarkers = undefined;

        }

    }

}

housingMap.js-meta.xml

<?xml version="1.0" encoding="UTF-8"?>

<LightningComponentBundle xmlns="http://soap.sforce.com/2006/04/metadata">

  <!-- Should match the org's API version; 59.0 corresponds to a specific Salesforce release -->

  <apiVersion>59.0</apiVersion>

  <!-- Must be true for the component to be selectable in Lightning App Builder -->

  <isExposed>true</isExposed>

  <targets>

    <!-- Makes the component draggable onto Home pages specifically.

         Other targets (lightning__RecordPage, lightning__AppPage, etc.) expose it elsewhere. -->

    <target>lightning__HomePage</target>

  </targets>

</LightningComponentBundle>


Quick Reference
Item
Value
LWC name
housingMap
Component type
JavaScript
Apex method wired
HouseService.getRecords
Base components used
lightning-card, lightning-map
Target
lightning__HomePage
API version
59.0



Key Concepts
@wire = declaratively binds a component property to a data source (an Apex method here); re-runs automatically when the source data changes, no manual refresh logic needed.
Base Lightning components (lightning-map, lightning-card) pre-built, Salesforce-maintained UI components that handle complex functionality (like Google Maps integration) without custom code.
@salesforce/apex/<Class>.<method> =the special import path LWC uses to call an @AuraEnabled Apex method as a plain JS function.
isExposed + targets = control where a component can be placed in Lightning App Builder; without them, the component exists but isn't selectable anywhere.


