# banoffee (333)
==================

## Initial Setup
Ensure the following are installed and up to date:
- [__node / npm__] (https://nodejs.org/en/download/)
- [__xcode__] (https://developer.apple.com/xcode/download/)

Fork the project template from Github and install the following:
- `$ sudo npm install -g bower cucumber cordova gulp ionic ios-deploy ios-sim strongloop`
- `$ sudo npm install`. This will grab all of the project dependencies.
- `$ gulp`. Running the default task from the Ionic directory will generate your `ionic/www/dist` folder.




## Configure Platforms
- Amend the __"widget id"__ in your __config.xml__ file. It must follow the following standard: 
	- `com.company.projectname` (e.g. com.cohaesus.onboardapp)


### iOS 
- Ensure Xcode is up to date.
- `$ ionic platform add ios`.


### Android
- Install the following:
	- [SDK Tools] (http://developer.android.com/sdk/index.html#Other).
	- [Java for OSX 2015-001] (https://support.apple.com/kb/DL1572?locale=en_US). 
	- [Java for OSX] (http://www.java.com/en/download/mac_download.jsp).
- Run the _android_ exec found in `android-sdk-macosx/tools`. Install the following: 
	- Desired Android SDK Platform(s)
	- Android SDK Tools
	- Android SDK Build Tools (>= v19.1.0)
	- SDK Platform Tools
	- Android Support Repository (found in Extras).
- Update __PATH__ in `~./bash_profile` to point to the Android SDK: 
	- Use either command to open *bash_profile*: `$ open -a TextEdit ~/.bash_profile` [Text Editor] or `$ nano ~/.bash_profile` [CLI]. 
	- Update the PATH inside the file, e.g. `export PATH=${PATH}:/Users/<COHAESUSEMPLOYEE>/Development/android-sdk-macosx/platform-tools:/Users/<COHAESUSEMPLOYEE>/Development/android-sdk-macosx/tools`. Make sure this path matches your *bash_profile* location. 
- Execute `$ source ~/.bash_profile` in the terminal.
- `$ ionic platform add android`




## Emulation
### Browser (live reload)
- In your ionic folder run `$ ionic serve` from the terminal.
- The Gulp Watch task will automatically run when you use the browser emulation. When changes made to any HTML, CSS, or JavaScript files are saved, Gulp will recompile your dist files and then automatically reload the browser.


### iOS (Mac only)
#### via Simulator
- Inside your ionic folder, build the app via the terminal `$ ionic build ios`
- Emulate the build `$ ionic emulate ios`.

#### via Connected Device
- Inside your ionic folder, build the app via the terminal `$ ionic build ios`
- `$ ionic run ios --device`


### Android
#### via Cordova
- Make sure [Java for Mac OSX] (http://www.java.com/en/download/mac_download.jsp) and the [Android SDK] (http://developer.android.com/sdk/installing/index.html?pkg=tools) are installed.
- Configure your Android devices via Tools > Manage AVDs in the Android SDK.
- Inside your ionic folder, build the app via the terminal `$ ionic build android`
- Emulate the build `$ ionic emulate android`


#### via GenyMotion [recommended]
- Create and verify a [Genymotion] (https://www.genymotion.com) account.
- [Download] (https://www.genymotion.com/download/) and install Genymotion.
- Add your desired devices to the program. Double click a device to launch (alternatively, highlight and press Start).
- Inside your ionic folder, build the app via the terminal `$ ionic build android`
- Emulate the build (with your device open in Genymotion) `$ ionic run android `




## CSS Framework
### SASS
- SASS structure is based on [Inverted Triangle CSS] (http://www.creativebloq.com/web-design/manage-large-css-projects-itcss-101517528) (ITCSS), courtesy of Harry Roberts.
- It is important that you import any files you create in the main.scss file are imported in the correct order. 
- Each folder contains a readme.md file, which explains the expected content.


### Bootstrap CSS
- The Bootstrap CSS library is a listed dependancy of the angular-ui-bootstrap module, so you also have access to the [Bootstrap CSS library] (http://getbootstrap.com/css/).
- An example jumbotron class has been included in `www/templates/search.html`.


### CSS
- We have left in a default _style.css_ in the `www/css` folder if you choose not to use SASS. You do not have to make any changes to the _index.html_ file, since _style.css_ is already imported into `scss/main.scss`. Note that all SASS files will overwrite the style.css stylesheet.




## Javascript 
### Angular-UI-Bootstrap
- We have installed Bootstrap components written in pure AngularJS. You can view the documentation [here] (https://angular-ui.github.io/bootstrap/).
- An example accordion has been included in `www/templates/search.html`.


### Browserify 
- We are using gulp-browserify to generate a single (minified) Javascript file that is referenced in index.html. 
- If you create any additional Javascript files, declare the file path at the top the page on `www/app.js` (referenced elsewhere as our single entry-point), and add any modular dependancies to the Angular _'starter'_ module. 
- This means you only ever need to reference `www/dist/js/app.min.js` in the _index.html_ file.


### Gulp Tasks
- `$ gulp` Default task. Runs the `$ gulp sass` and `$ gulp scripts` tasks.
- `$ gulp scripts` Uses [browserify] (https://www.npmjs.com/package/gulp-browserify) to pull all JS files declared in your single-point entry (and their associated depandancies) and [annotates] (https://www.npmjs.com/package/gulp-ng-annotate) them. It then generates your `www/dist/js/app.js` and an [uglified] (https://www.npmjs.com/package/gulp-uglify) `www/dist/js/app.min.js` file. 
- `$ gulp sass` Compiles all Sass/CSS files declared in `scss/main.scss`, then generates the `www/dist/css/main.css` and a [minified] (https://www.npmjs.com/package/gulp-minify-css) `www/dist/css/main.min.css`.
- `$ gulp deploy-Android` / `$ gulp deploy-iOS` Increments the build version (using git tags), generates a new platform build, deploys it to HockeyApp, and publishes the build information in your HipChat project room. 




## HockeyApp
### Setup
- We are using Hockeyapp to distribute builds to approved devices. 
- Create a HockeyApp [account] (https://rink.hockeyapp.net/registrations/new).
- Request an invitation to the Cohaesus HockeyApp account (See Richard Bundock).
- Create a New App for each platform from the HockeyApp Dashboard (select create the app manually).
- The Bundle Identifier (iOS) / Package Name (Android) must match the __widget id__ in your __config.xml__ file. 
- Collect the App ID (located by selecting the app from the dashboard) and [generate an API token] (https://rink.hockeyapp.net/manage/auth_tokens) for your app. Assign the values to the respective variables in the deploy-scripts folder.


### Adding a Device
- You can add a device to your HockeyApp profile by accessing [Devices] (https://rink.hockeyapp.net/manage/devices) from the Dashboard.
- Select _Guided Process_.
- HockeyApp will generate a link for you to access on your mobile device. 
- Accessing this link from your mobile device will add it to either your profile's provisioned or unprovisioned devices, depending on whether your device has been provisioned on the account you used to generate the platform file.
- You can add unprovisioned devices to your provisioning profile by following [these instructions] (http://support.hockeyapp.net/kb/client-integration-ios-mac-os-x-tvos/adding-new-devices-to-your-provisioning-profile).


### Distribution (__important__)
- Select _Manage App_ inside your newly-created app. From there, navigate to _Distribution_ and set the Download page to __private__. This ensures anyone with the URL and anyone whose UDID is in the provisioning profile will not be able to access and download the app. 
- To prevent other devices provisioned on our Apple Developer account being able to download your app, you will either need to add your __TEAMID__ as a parameter in your _deploy-android.sh_ and _deploy-ios.sh_.
- You can find your team's Database ID in HockeyApp by navigating to Teams from the Dashboard and clicking on your team. The team ID is in the url. 


### Deployment
#### Android (.apk)
##### Initial Deployment
- Run `$ ionic build --release android`
- Follow [these instructions] (http://ionicframework.com/docs/guide/publishing.html) to generate and sign the .apk file.
- Executing `$ keytool -genkey -v -keystore my-release-key.keystore -alias alias_name -keyalg RSA -keysize 2048 -validity 10000` will generate your keystore file in the directory you executed the command. _.gitignore_ is set to ignore keystore files stored in the ionic folder, if you choose to store it outside of the apk folder. 
- Sign your app with `$ jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore my-release-key.keystore android-release-unsigned.apk alias_name`
- Update the __deploy-android.sh__ and __deploy-tags.sh__ scripts in the deploy-scripts folder. When uploading to HockeyApp, make sure the __APP_FILE__ is set to the __android-release-unsigned.apk__ file.
- Run the deploy-Android Gulp task `$ gulp deploy-Android`. 

###### Publishing to Google Play Store
- To use the zipalign command `$ zipalign -v 4 android-release-unsigned.apk <App Name>.apk`, copy the zipalign file from android-sdk-macosx/build-tools and paste in android-sdk-macosx/tools. Only use the zipalign command if are publishing to the Google Play store. 

##### Future Deployment
- Commit and push your changes to the repo (New commits are required to increment the build version).
- Run the deploy-Android Gulp task `$ gulp deploy-Android`


#### iOS (.ipa)
##### Initial Setup
- In the ionic directory, run `$ ionic build ios`.
- Request an invitation to the 'Cohaesus Projects Ltd' Apple Developer Account (see Richard Bundock).
- Navigate to Xcode > Preferences > Account.
- Import your developer profile using the cog, or add your Apple ID using the plus (after accepting the Cohaesus invitation). 
- Open Xcode. Import the __.xcodeproj__ file generated from `$ ionic build ios`, found in `platforms/ios`.
- Select Product > Clean.
- In Xcode, click on your App on the sidebar on the left hand side of the page. 
- Under _General_, locate _Team_ in the _Identity_ section. 
- If you can see the following error: _“Missing iOS Distribution signing identity for …”_, click the __Fix this Issue__ button. 
- Run the deploy-iOS Gulp task `$ gulp deploy-iOS`.
- If the gulp task still fails, [this] (http://stackoverflow.com/questions/32821189/xcode-7-error-missing-ios-distribution-signing-identity-for) fix should resolve the error. Re-run the deploy-iOS Gulp task `$ gulp deploy-iOS`.


##### Future Deployment
- Commit and push your changes to the repo (Commiting is required to increment the build version).
- Run the deploy-iOS Gulp task `$ gulp deploy-iOS`.





## API
- You will need node.js, if you don't have it already,  for the backend API
- You will also the express framework for node
	- ``` $ npm install express --save ```
- You will also need loopback for creating your APIs quickly
	- ``` slc loopback ```
	- To access the gui editor for making your models type:
		- ``` slc arc ```
		- Otherwise you can use the CLI
	- You will need to install the connector for your db of choice
	- ``` npm install loopback-connector-postgresql --save ```
- You will need a Database, you can use heroku, or something local to get started
	- (we reccomend postgreSQL, as it is easier to manipulate the data structure of relational databases as you go along.)




## Testing
For Testing we are using the following:
- [gherkin](https://github.com/cucumber/cucumber/wiki/Gherkin): for BDD to write in human-readable language (especially useful for non-techies)
- [cucumber](https://github.com/cucumber/cucumber-js): takes gherkin syntax and converts it into JS
- [protractor](http://www.protractortest.org/#/): for End2End testing in Angular.js
- [mocha](https://www.npmjs.com/package/mocha): a popular assertion library in JS.

### Doing tests:
1. Write your gherkin tests in `ionic/features/*.feature`
2. then create a JS file in step_definition with the same name underscore steps.js (see example in features folder)
3. run `gulp cucumber`, you could also run `cucumber.js`
4. then copy the gherkin converted js code and paste it into the JS file you created in step_definitions, now you can add your assertions etc.




## Database
- PostgreSQL + pg (npm package) + knex (query builder)
- MongoDB + Mongoose
