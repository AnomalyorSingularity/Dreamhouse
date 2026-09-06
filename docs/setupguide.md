Get Ready to Develop Setup Guide & Reference
Salesforce Trailhead Project: DreamHouse Realty (Unit 1)
A complete walkthrough for setting up your Salesforce development environment, plus a quick-reference section for future setups.


About This Exercise
This project prepares you to build a feature for DreamHouse Realty, a fictitious real estate company, that lets agents manage available houses and visualize them on a map. You'll set up your tools, build a data model, write backend logic in Apex, and build a front-end feature with Lightning Web Components (LWC).

Learning objectives:

Set up a Salesforce development environment
Create a data model in Salesforce
Write Apex code to retrieve data from Salesforce objects
Create and deploy a Lightning web component (LWC)

This guide covers the setup phase only — the environment you need before any of that development work begins.


Tools You'll Need
Tool
Purpose
Trailhead Playground
Your Salesforce dev org
Salesforce CLI
Manages the app development lifecycle from the command line
Visual Studio Code
Code editor
Salesforce Extension Pack (Expanded)
VS Code extensions for Salesforce dev
JDK 21 (recommended)
Powers the Apex Language Server in VS Code
Node.js (Active LTS)
Needed for LWC tooling and project scripts



Step-by-Step Setup
1. Create a New Trailhead Playground
Scroll to the bottom of the Trailhead module page, click the Playground name, then click Create Playground. Provisioning takes 3–4 minutes.

Important: Always use a brand-new Playground for this project. Reusing an existing org can cause challenge checks to fail later, since it may already contain conflicting objects or code.

How to confirm it's actually new:

Setup → Company Information → check the Created Date matches today
Setup → Object Manager → a fresh Playground has no custom objects
Terminal: sf org list shows all orgs you've authorized, with aliases
2. Reset Your Playground Password
Click the App Launcher, search for and open Playground Starter.
Open the Get Your Login Credentials tab to see your username.
Click Reset My Password → OK. Check your email.
Click the emailed link, set a new password, confirm it.

You'll need this password to log in from the CLI and VS Code — it's separate from your Trailhead login.
3. Install Salesforce CLI
Download and install from the Salesforce CLI Setup Guide for your OS.

Verify installation:

sf update
4. Install VS Code + Salesforce Extension Pack (Expanded)
Install Visual Studio Code.
Click the Extensions icon in the left toolbar.
Search Salesforce Extension Pack (Expanded) → Install.
5. Install a JDK (Required for Apex Support)
The Apex Language Server needs a JDK. Salesforce currently recommends JDK 21, and supports any version 11+.

Check your chip type: Apple menu → About This Mac (Apple Silicon vs. Intel), or on Windows check System Info.
Download Temurin JDK 21 from adoptium.net — pick the installer matching your OS/chip.
Run the installer with default options.
Open a new terminal window and verify:

java -version

In VS Code, run Developer: Reload Window from the Command Palette so the extension detects it.

(See the Troubleshooting section below if VS Code still can't find Java.)
6. Create and Connect Your Salesforce Project
Open VS Code → Command Palette (Ctrl/Cmd+Shift+P) → SFDX: Create Project.
Choose Standard, name it Dreamhouse, and pick a folder.
Command Palette → SFDX: Authorize an Org → choose Production → set alias to myDevOrg.
A browser window opens — log in with your Playground credentials and click Allow.

Use exactly myDevOrg as the alias — later steps in this project reference it by name.
7. Install Node.js (Active LTS)
Download from nodejs.org.

Verify:

node --version
8. Install Project Tooling
In VS Code, open the Command Palette → View: Toggle Terminal.
Run:

npm install

Command Palette → Developer: Reload Window.

At this point your environment is fully set up. No coding has happened yet — the next units in the trail cover the data model, Apex, and LWC work.


Quick Command Reference
Task
Command
Update Salesforce CLI
sf update
Check Node.js version
node --version
Check Java version
java -version
List all authorized orgs
sf org list
Open your connected org in browser
sf org open
Install project npm packages
npm install


Command Palette shortcuts used: Ctrl/Cmd+Shift+P opens it. Key commands: SFDX: Create Project, SFDX: Authorize an Org, View: Toggle Terminal, Developer: Reload Window.

Key project names to remember:

Project name: Dreamhouse
Org alias: myDevOrg


Troubleshooting
"Unable to locate a Java Runtime" (macOS)
This means no JDK is installed on your machine.

Confirm your Mac's chip type via About This Mac.
Download and install Temurin JDK 21 from adoptium.net (pick the installer matching your chip).
Open a brand-new terminal window (not a reused one) and run java -version to confirm.
In VS Code, run Developer: Reload Window.
If it's still not detected, manually point VS Code to it:
Open Settings (Cmd+,) → search apex java home
Set salesforcedx-vscode-apex.java.home to:

/Library/Java/JavaVirtualMachines/temurin-21.jdk/Contents/Home

Reload the window again.
General Tips
After installing any CLI tool or JDK, open a new terminal window — old ones won't see updated PATH/environment variables.
After installing or updating a VS Code extension, run Developer: Reload Window rather than relying on it to pick up changes automatically.
If sf org list doesn't show myDevOrg, the authorization step likely didn't complete — repeat Step 6.



