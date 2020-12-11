# Table of Contents
- [Whats UAUP](#whats-uaup-js)
- [Installation](#installation)
- [Getting Started](#getting-started)
- [Creating an Update](#creating-an-update)
- [How It Works](#how-it-works)

# Whats UAUP-JS
UAUP or Universal Auto Update Platform, is a framework for NodeJS that allows you to easily create an auto updater for any desktop application using either base NodeJS or Electron. 
You do **NOT** need the base application to be created in nodejs.  It just needs an executable to call apon.

# Installation
Since UAUP does require NodeJS to function we cannot use a CDN.
Instead we need to use NPM
```
npm i uaup-js --save
```

# Getting Started
### Import
```javascript
const uaup = require('uaup-js');
```

### Update Object

```javascript
let updateOptions = {
    useGithub: true, //Only Github is Currenlty Supported. {Default is true} [Optional]
    gitRepo: "uaup-js", // Your Repo Name [Required]
    gitUsername: "billy123",  // Your GitHub Username [Required]
    isGitRepoPrivate: false,  // If the Repo is Private or Public  (Currently not Supported) {Default is false} [Optional]
    gitRepoToken: "abc123",  // The Token from GitHub to Access a Private Repo.  Only for Private Repos {Default is null} [Optional]

    appName: "uaup-js", // The Name of the app [Required]
    appExecutableName: "UAUP JS.exe", // The Executable of the Application to be Run after updating [Required]

    appDirectory: "/path/to/application", // Where the app will receide, make sure your app has permissions to be there.  [Required]
    versionFile: "/path/to/version.json", // The Path to the Local Version File. {Default is "Application directory/settings/version.json"} [Optional]
    tempDirectory: "/tmp", // Where the Update archive will download to. {Default is "Application directory/tmp"} [Optional]
    optionsDirectory: "DO NOT CHANGE", {Default is the versionFile Parent Directory} [DO NOT CHANGE]

    progressBar: null, // If Using Electron with a HTML Progressbar, use that element here, otherwise ignore {Default is null} [Optional]
    label: null, // If Using Electron, this will be the area where we put status updates using InnerHTML {Default is null} [Optional]
    forceUpdate: false // If the Application should be forced updated.  This will change to true if any errors ocurr while launching. {Default is false} [Optional]
};
```

### Update
```javascript
// This will check for updates, download and install (if found), and launch the application.
// If no update was found the application will launch
// If the Launch Executable is not found the application will force update
uaup.Update(updateObject);
```

### Manually Check For Updates
This is not required, but sometimes you want to check for updates with out updating.

```javascript
let isUpdateAvalible = uaup.CheckForUpdates(updateOptions);
if(isUpdateAvalible){
    // Do STUFF HERE
}
```
# Creating an Update
To Create an Update package your application in a zip archive and create a Git Release using the Tag Option as the Application Version
### Example
1. Package Application.
1. Create a Github Release.
1. Set the Tag Option to the Application Version.
1. Publish

# How It Works
UAUP-JS Using the GitHub API to check if the current releases tag matches the last recorded tag, if they differ an update is needed, if there the same than we continue launching the application.
