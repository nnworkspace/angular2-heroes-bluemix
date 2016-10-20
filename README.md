# _Tour of Heroes_ in IBM&reg; Bluemix&reg;

[_Tour of Heroes_, the official tutorial of Angular 2][tour_of_heroes] teaches the quintessential aspects of AngularJS 2, such as data services, routing (application navigation), and HTTP. It is an ideal start point for anyone who would like to learn Angular 2, and the source code of the heroes application also serves as a good template for an initial setup of an Angular 2 application.  

[A while ago I went through this tutorial and have it deployed on IBM Bluemix][app_url] (this link may be invalid after a few days, because I'm going to delete it from my bluemix account to free up resources). This post is a tutorial about how to get your Angular 2 heroes up and running on Bluemix. 

This project is extended from [Frederic Lavigne's bluemix-hello-angular2 project][bluemix_hello_angular2_github]. Many thanks to Mr. Lavigne!

## Prerequisites

1. If you haven't gone through the official [_Angularjs 2 Quickstart_][angular2_quick_start] and the [_Tour of Heroes Tutorial_][tour_of_heroes], by all means do it. Install all the runtimes and additional libraries that is described in the Quickstart.

1. Install Git. Use Git Bash or any other Git shell for running npm tasks even if you are using a windows box. 

1. Install [angular-cli][angular_cli] for building deployables. 

  ```
  npm install -g angular-cli
  ```

1. [Sign up a Bluemix account][bluemix_signup_url], or use an existing one. 

1. Install [bluemix-cli][bluemix_cli] for connecting to bluemix.    

1. Install [cloudfoundry-cli][cloud_foundry_url] for deployment of your applications.  


## Project Local Build

1. Clone the source code of the "Angular 2 Heroes on Bluemix" app to your local directory. Let's call it <path-to-your-heroes>. 

  ```
  git clone https://github.com/nnworkspace/angular2-heroes-bluemix
  ```

1. Cd into your project directory.

1. Fetch angular-cli tooling libraries that are needed for building the deployables: 
  ```
  ng init
  ```
  If you are asked any questions like "packages.json already exists, overwrite?", answer all those questions with no. I have already written and tested the configuration files, and these config files should not be overwritten by the angular-cli default values. The mere purpose of this step is fetching the building dependencies to your project directory. Without this step, the `ng build` in the script section of the `packages.json` will fail.   

1. Install the project dependencies:

   ```
   npm install
   ```

1. Build the project:

  ```
  npm run dist
  ```

  This task is defined in [`package.json`](package.json). It compiles the source code written in TypeScript into deployable JavaScript. In this example, we make bluemix serve plain HTML, CSS, JavaScript files. In addition it copies the bluemix [`manifest.yml`](manifest.yml) file to the **`dist`** directory together with the [Staticfile](Staticfile). Those two are needed to deploy the **`dist`** folder with the [Cloud Foundry static buildpack](https://github.com/cloudfoundry/staticfile-buildpack).

1. Run the project locally, to see whether everything works as described in the [_Tour of Heroes Tutorial_][tour_of_heroes]:

  ```
  ng serve
  ```
  The test URL is [`http://localhost:4200/`](http://localhost:4200/).



## Heroes on Cloud a la Bluemix

1. Cd into the dist directory after build and local test:

  ```
  cd dist
  ```

1. Connect to IBM Bluemix:

  ```
  bluemix api https://api.eu-gb.bluemix.net
  ```

1. Login to Bluemix:

  ```
  bluemix login -u <your-user-account> -o <your-organization> -s <your-space>
  ```
  If you are using a federated ID, use the -sso option:
  ```
  bluemix login -u <your-user-account> -o "<your-organization>" -s "<your-space>" -sso
  ```

1. Up onto the cloud:

  ```
  cf push
  ```
  It will create a new app named *angular2-heroes* with a random route. Watch for the route name in the `cf push` output.


## Troubleshooting


To troubleshoot your Bluemix app the main useful source of information is the logs. To see them, run:

  ```
  cf logs <application-name> --recent
  ```


## Extended Reading

Joe Deluca also made an Angluar 2 project [_petstore-client-angular2_][petstore_angular2_github] run on Bluemix. You may want to have a look. 



----------------------------------
The program is provided as-is with no warranties of any kind, express or implied.

[app_url]: https://angular2-heroes-pseudoviscous-satisfactoriness.eu-gb.mybluemix.net
[bluemix_hello_angular2_github]: https://github.com/l2fprod/bluemix-hello-angular2
[angular2_quick_start]: https://angular.io/docs/ts/latest/quickstart.html
[tour_of_heroes]: https://angular.io/docs/ts/latest/tutorial/
[angular_cli]: https://github.com/angular/angular-cli
[bluemix_signup_url]: https://console.ng.bluemix.net/registration/?Target=https%3A%2F%2Fconsole.ng.bluemix.net%2Flogin%3Fstate%3D%2Fhome%2Fonboard
[bluemix_cli]: https://clis.ng.bluemix.net/ui/home.html
[cloud_foundry_url]: https://github.com/cloudfoundry/cli
[petstore_angular2_github]: https://github.com/joeydeluca/petstore-client-angular2
