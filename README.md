# Design Automation - Migration Guide from V2 to V3 

[![Design-Automation](https://img.shields.io/badge/Design%20Automation-v3-lightblue.svg)](http://forge.autodesk.com/)

![Basic](https://img.shields.io/badge/Level-Basic-green.svg)
[![License](http://img.shields.io/:license-MIT-blue.svg)](http://opensource.org/licenses/MIT)

# Description

Design Automation of Forge V2 only supports AutoCAD engine. This migration guide maps the API changes from [V2](https://forge.autodesk.com/en/docs/design-automation/v2/developers_guide/overview/) to [V3](https://forge.autodesk.com/en/docs/design-automation/v3/developers_guide/overview/), how to migrate and what's new on `v3`.

Key concepts remain the same: the `AppBundle` (formerly `AppPackage`) contains the custom code of plugin, the `Activity` determines how to run it, and the `Workitem` is the execution job with input and output specification. `Engines` now supports more products (AutoCAD, Inventor, Revit, 3DsMax).

![](/thumbnail.png)

# Sections

## API Changes :card_index:

This section maps the v2 endpoints with the new v3 endpoints.

- [AppBundles](apppackages.md), formerly AppPackages
- [Activities](activities.md)
- [Worktems](workitems.md)
- [Engines](engines.md)

## New API Groups in V3 :new:

This section lists what's new with links to the documentation.

- Forge Apps
  - [GET forgeapps/:id](https://forge.autodesk.com/en/docs/design-automation/v3/reference/http/forgeapps-id-GET/)
  - [DELETE forgeapps/:id](https://forge.autodesk.com/en/docs/design-automation/v3/reference/http/forgeapps-id-DELETE/)
  - [PATCH forgeapps/:id](https://forge.autodesk.com/en/docs/design-automation/v3/reference/http/forgeapps-id-PATCH/)
- Health 
  
  - [GET health/:engine](https://forge.autodesk.com/en/docs/design-automation/v3/reference/http/health-engine-GET/)
- ServiceLimits
  - [GET servicelimits/:owner](https://forge.autodesk.com/en/docs/design-automation/v3/reference/http/servicelimits-owner-GET/)
  - [PUT servicelimits/:owner](https://forge.autodesk.com/en/docs/design-automation/v3/reference/http/servicelimits-owner-PUT/)
- Shares
  
  - [GET shares](https://forge.autodesk.com/en/docs/design-automation/v3/reference/http/shares-GET/)

## Packages (v3)

- [.NET](https://www.nuget.org/packages/Autodesk.Forge.DesignAutomation/) on nuget ([source](https://github.com/Autodesk-Forge/forge-api-dotnet-design.automation))
- [Nodejs](https://www.npmjs.com/package/autodesk.forge.designautomation) on npm ([source](https://github.com/Autodesk-Forge/Autodesk.Forge.DesignAutomation))
 
# Further Reading

Documentation:

- [Design Automation Overview](https://forge.autodesk.com/en/docs/design-automation/v3/developers_guide/overview/) (v3)

Tutorial:

- [Design Automation for AutoCAD tutorial](https://forge.autodesk.com/en/docs/design-automation/v3/tutorials/autocad/)

 
## License

This sample is licensed under the terms of the [MIT License](http://opensource.org/licenses/MIT). Please see the [LICENSE](LICENSE) file for full details.

## Written by

Madhukar Moogala [@galakar](https://twitter.com/galakar), [Forge Advocate](http://forge.autodesk.com)

