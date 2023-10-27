# Acrolinx-Installer-for-AEMaaCS

[![Maven Central](https://img.shields.io/maven-central/v/com.acrolinx.client/acrolinx-for-aem.all)](https://search.maven.org/artifact/com.acrolinx.client/acrolinx-for-aem.all)

## Steps for Adding Acrolinx to AEMaaCS

Follow this step-by-step guide to integrate Acrolinx to your existing code repository.

## Adding the Acrolinx Module

- Create a clone of your Cloud Manager's Git repository.
- Copy the Acrolinx module from this repository to the root directory of the cloud manager code.
- Update  **/acrolinx/pom.xml**

  - Replace the parent pom section with your parent's pom details, as shown below:
    - Example shows adding to `aem-guides-wknd` sample project

  ![Parent Section of Module](assets/parent-section.png)

  - Update the artifact Id as per your application's naming convention:

  ![Artifact ID](assets/artifact-id-manager.png)

- Update  **/acrolinx/acrolinx.installer/pom.xml**

  - Update the artifact id as per your application's naming conventions.

  ![Artifact ID](assets/artifact-id-installer.png)

- Add the Acrolinx module in the parent pom module section.

  ![Parent POM](assets/parent-pom.png)

- Add a dependency to `all` module for acrolinx installer

  In the `all` module's pom.xml add:

  ```xml
  <dependency>
    <groupId>com.acrolinx.client</groupId>
    <artifactId>aemaacs-acrolinx-project-acrolinx-installer</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <type>zip</type>
  </dependency>
  ```

  In the plugin section of the `all` module under the `filevault-package-maven-plugin` add an `embedded` section similar to other modules.

  ```xml
  <embeddeds>
    <embedded>
      <groupId>com.acrolinx.client</groupId>
      <artifactId>aemaacs-acrolinx-project-acrolinx-installer</artifactId>
      <type>zip</type>
      <target>/apps/wknd-packages/application/install</target> <!-- Adjust path as per your project-->
    </embedded>
  </embeddeds>
  ```

## Acrolinx Configuration
In cloud manager configuration add the following environment variables.

| NAME | VALUE | TYPE |
|------|-------|------|
|`ACROLINX_URL`| `https://<tenant>.acrolinx.cloud`| variable |
|`ACROLINX_GENERIC_TOKEN`|`secret-token`|secret|

### Optional Configuration 

Refer the "Configure Acrolinx Access" section in the [documentation](https://support.acrolinx.com/hc/en-us/articles/10211388159378-Admin-Guide) before updating the value.

| NAME | VALUE | TYPE | DEFAULT |
|------|-------|------|---------|
|`ACROLINX_ALLOWED_REGEX`|`your-site-name`| variable | `.*` |
|`ACROLINX_FORWARD_COOKIES`|`true` or `false`| variable |`false`|
|`ACROLINX_LOG_LEVEL`|`DEBUG`| variable |`INFO`|
|`ACROLINX_SIDEBAR_SITES`|`true` or `false`| variable |`true`|

Example:

![Configuration](assets/configuration.png)

## Updating Acrolinx

Update `acrolinx.version` property in **/acrolinx/acrolinx.installer/pom.xml**

Example: `<acrolinx.version>2.3.0</acrolinx.version>`

## Uninstalling Acrolinx

- Remove the Acrolinx module from your cloud project.
- Remove entries from parent pom.xml in your project.
- Remove cloud configuration for Acrolinx URL, generic token.
- Rerun cloud manager pipeline.

## Requirements

Guides for AEM as Cloud Service: `2023.10.0.373` <https://experienceleague.adobe.com/docs/experience-manager-guides-learn/tutorials/release-info/latest-release-info.html?lang=en>

## License

Copyright 2022-present Acrolinx GmbH

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at:

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

For more information visit: [https://www.acrolinx.com](https://www.acrolinx.com)
