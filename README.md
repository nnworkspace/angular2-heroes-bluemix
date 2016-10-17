Tour of Heroes, the official tutorial of Angular 2 teaches the quint essential aspects of AngularJS 2, such as data services, routing (application navigation), and HTTP. It is an ideal start point for anyone who would like to learn Angular 2, and the source code of the heroes application also serves as a good template for an initial setup of an Angular 2 application.  

A while ago I went through this tutorial and got it deployed on IBM Bluemix. [The application is running like a charm](http://angular2-heros-pugilistical-curb.eu-gb.mybluemix.net/). This post is a tutorial about how to get your Angular 2 heroes up and running on Bluemix.   

Prerequisits: 

1. If you haven't gone through the official Angularjs 2 Quickstart and the "Tour of Heroes" tutorial , by all means do it. Install all the runtimes and additional libraries that is described in the Quickstart. (add links here)

2. Install Git. Use Git Bash for running npm tasks even if you are using a windows box. 

3. Install [angular-cli](https://github.com/angular/angular-cli) for building deployables. 

```
npm install -g angular-cli
```

4. Register a Bluemix account. It's free. 

5. Install [bluemix-cli](Url to bluemix cli) for connecting to bluemix.    

6. Install [cloudfoundry-cli](url to cloud foundry) for deployment of your applications.  


# Heros on Bluemix

1. Clone the source code of the "Angular 2 Heroes on Bluemix" app to your local directory. Let's call it <path-to-your-heroes>. 

  ```
  git clone https://github.com/nnworkspace/
  ```

2. Cd into <path-to-your-heroes>

3. Fetch angular-cli tooling libraries that are needed for building the deployables. 
  ```
  ng init
  ```
  If you are asked any questions like "packages.json already exists, overwrite?", answer all those questions with no. I have already written and tested the configuration files, and these config files should not be overwritten by the angular-cli default values. The mere purpose of this step is fetching the building dependencies to your project directory. Without this step, the "ng build" in later step will fail.   

4. Install the project dependencies:

   ```
   npm install
   ```

1. Build the project

  ```
  npm run dist
  ```

  This task is defined in [package.json](package.json). It compiles the source code written in TypeScript into deployable JavaScript. Bluemix currently does not suppurt "transpiler" yet, we have to go this way for now. In addition it copies the bluemix [manifest.yml](manifest.yml) file to the **dist** directory together with the [Staticfile](Staticfile). Those two are needed to deploy the **dist** folder with the [Cloud Foundry static buildpack](https://github.com/cloudfoundry/staticfile-buildpack) making it possible to serve plain HTML, CSS, JavaScript files.


--------------------------------------------------------------------------------

# Angular 2 in IBM Bluemix

This project deploys a simple Angular 2 app in IBM Bluemix. The Angular 2 uses the [angular-cli](https://github.com/angular/angular-cli) to generate the application artifacts into the **dist** folder. Once generated, these artifacts are deployed to IBM Bluemix and served by the [Cloud Foundry static buildpack](https://github.com/cloudfoundry/staticfile-buildpack).

## Running the app on Bluemix

1. Create a Bluemix Account

    [Sign up][bluemix_signup_url] for Bluemix, or use an existing account.

2. Download and install the [Cloud-foundry CLI][cloud_foundry_url] tool

3. Clone the app to your local environment from your terminal using the following command

  ```
  git clone https://github.com/l2fprod/bluemix-hello-angular2.git
  ```

4. Cd into this newly created directory

1. Install [angular-cli](https://github.com/angular/angular-cli)

  ```
  npm install -g angular-cli
  ```

1. Install the project dependencies

  ```
  npm install
  ```

1. Build the project

  ```
  npm run dist
  ```

  This task defined in [package.json](package.json) compiles the Angular 2 app. In addition it copies the [manifest.yml](manifest.yml) file to the **dist** directory together with the [Staticfile](Staticfile). Those two are needed to deploy the **dist** folder with the [Cloud Foundry static buildpack](https://github.com/cloudfoundry/staticfile-buildpack) making it possible to serve plain HTML, CSS, JavaScript files.

1. Change to the dist directory

  ```
  cd dist
  ```

1. Push the application to Bluemix

  ```
  cf push
  ```

  It will create a new app named *bluemix-hello-angular2* with a random route. Watch for the route name in the ```cf push``` output.


This project was generated with [angular-cli](https://github.com/angular/angular-cli) version 1.0.0-beta.15.

## Troubleshooting

To troubleshoot your Bluemix app the main useful source of information is the logs. To see them, run:

  ```
  cf logs <application-name> --recent
  ```

---

This project is a sample application created for the purpose of demonstrating the deployment of a Angular 2 app in IBM Bluemix.
The program is provided as-is with no warranties of any kind, express or implied.

[bluemix_signup_url]: https://console.ng.bluemix.net/?cm_mmc=GitHubReadMe-_-BluemixSampleApp-_-Node-_-Workflow
[cloud_foundry_url]: https://github.com/cloudfoundry/cli
