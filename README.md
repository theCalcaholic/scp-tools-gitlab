# SAP Cloud Platform Tools optimized for GitLab Runner

> One image to rule them all

## Software

This Docker image based is on Ubuntu GNU/Linux.

The following software is included:

* [SapMachine](https://sap.github.io/SapMachine/) *OpenJDK release maintained and supported by SAP* (`java`)
* [Cloud Foundry CLI](https://docs.cloudfoundry.org/cf-cli/) (`cf`)
* [SAP Cloud Platform Neo Environment SDK](https://tools.hana.ondemand.com/#cloud) (`neo.sh`)
* [SAP Multi-Target Application Archive Builder](https://help.sap.com/viewer/58746c584026430a890170ac4d87d03b/Cloud/en-US/ba7dd5a47b7a4858a652d15f9673c28d.html) (`mta_archive_builder.jar`)
* [Node.js](https://nodejs.org/) (`node`)
  * [grunt-cli](https://www.npmjs.com/package/grunt-cli)
  * [gulp-cli](https://www.npmjs.com/package/gulp-cli)
    * [ui5-toolkit-gulp](https://www.npmjs.com/package/ui5-toolkit-gulp)
  * [showdown](https://www.npmjs.com/package/showdown)
  * [eslint](https://www.npmjs.com/package/eslint)
    * [eslint-plugin-ui5](https://www.npmjs.com/package/eslint-plugin-ui5)
    * [eslint-config-ui5](https://www.npmjs.com/package/eslint-config-ui5)

## HOWTO

Execute...

* Java: `java`
* Cloud Foundry CLI: `cf`
* SAP Cloud Platform Neo Environment SDK: `neo.sh`
* SAP Multi-Target Application Archive Builder: `java -jar $MTA_BUILDER_HOME/mta_archive_builder.jar`
* Node.js: `node`

### Example

`.gitlab-ci.yml`:

```
image: cyclenerd/scp-tools-gitlab:latest

stages:
  - deploy

build-and-deploy:
  stage: deploy
  script:
    - java -jar $MTA_BUILDER_HOME/mta_archive_builder.jar --mtar deploy.mtar --build-target=NEO build
    - neo.sh deploy-mta -a "$SCP_ACCOUNT" -u "$SCP_USER" -p "$SCP_PASSWORD" -h hana.ondemand.com --source deploy.mtar --synchronous
  only:
    - master
```

## Help 👍

If you have found a bug (English is not my mother tongue) or have any improvements, send me a pull request.
