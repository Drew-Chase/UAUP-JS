# Table of Contents
- [Whats UAUP](#whats-uaup-js)
- [Installation](#installation)
- [Getting Started](#getting-started)
- [Creating an Update](#creating-an-update)
- [How It Works](#how-it-works)
- [Video](#video-tutorial)

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

### Stages

```javascript
const defaultStages = {
    Checking: "Checking For Updates!", // When Checking For Updates.
    Found: "Update Found!",  // If an Update is Found.
    NotFound: "No Update Found.", // If an Update is Not Found.
    Downloading: "Downloading...", // When Downloading Update.
    Unzipping: "Installing...", // When Unzipping the Archive into the Application Directory.
    Cleaning: "Finalizing...", // When Removing Temp Directories and Files (ex: update archive and tmp directory).
    Launch: "Launching..." // When Launching the Application.
};

```


### Update Object

```javascript


const updateOptions = {
    useGithub: true, // {Default is true} [Optional] Only Github is Currenlty Supported.
    gitRepo: "uaup-js", // [Required] Your Repo Name
    gitUsername: "billy123",  // [Required] Your GitHub Username.
    isGitRepoPrivate: false,  // {Default is false} [Optional] If the Repo is Private or Public  (Currently not Supported).
    gitRepoToken: "abc123",  // {Default is null} [Optional] The Token from GitHub to Access a Private Repo.  Only for Private Repos.

    appName: "uaup-js", //[Required] The Name of the app archive and the app folder.
    appExecutableName: "UAUP JS.exe", //[Required] The Executable of the Application to be Run after updating.

    appDirectory: "/path/to/application", //{Default is "Application Data/AppName"} [Optional]  Where the app will receide, make sure your app has permissions to be there.
    versionFile: "/path/to/version.json", // {Default is "Application directory/settings/version.json"} [Optional] The Path to the Local Version File.
    tempDirectory: "/tmp", // {Default is "Application directory/tmp"} [Optional] Where the Update archive will download to.

    progressBar: null, // {Default is null} [Optional] If Using Electron with a HTML Progressbar, use that element here, otherwise ignore
    label: null, // {Default is null} [Optional] If Using Electron, this will be the area where we put status updates using InnerHTML
    forceUpdate: false, // {Default is false} [Optional] If the Application should be forced updated.  This will change to true if any errors ocurr while launching.
    stageTitles: defaultStages, // {Default is defaultStages} [Optional] Sets the Status Title for Each Stage
};
```

### Update
```javascript
// This will check for updates, download and install (if found), and launch the application.
// If no update was found the application will launch
// If the Launch Executable is not found the application will force update
uaup.Update(updateOptions);
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


# Video Tutorial
[![Alt text](https://img.youtube.com/vi/FETAvJrnHK4/0.jpg)](https://youtu.be/FETAvJrnHK4)

