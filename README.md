# Ngapp02

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 6.0.3.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Production server on azure

To deploy to an azure web app with no .net:
(reference https://www.newventuresoftware.com/blog/deploying-angular-4-cli-apps-to-iis-on-azure )

1) Run `ng build --prod`
2) create a web.config in dist/ngapp02/
  contents:

<?xml version="1.0"?>

<configuration>
    <system.webServer>
        <staticContent>
            <mimeMap fileExtension=".json" mimeType="application/json" />
            <mimeMap fileExtension=".woff" mimeType="application/x-font-woff" />
            <mimeMap fileExtension=".woff2" mimeType="font/woff2" />
        </staticContent>
    </system.webServer>
    <system.webServer>
    <rewrite>
        <rules>
            <rule name="angular cli routes" stopProcessing="true">
                <match url=".*" />
                <conditions logicalGrouping="MatchAll">
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
                    <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
                </conditions>
                <action type="Rewrite" url="/" />
            </rule>
        </rules>
    </rewrite>
  </system.webServer>
</configuration>

3) delete contents of azure web app's /wwwroot folder (except hostingstart.html and web.config, if present)
4) copy contents (via ftp) of dist/ngapp02/ to azure web app's /wwwroot folder. 
(the web.config file disappears from dist/<app> upon subsequent builds, but it'll be up on server.)

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).
