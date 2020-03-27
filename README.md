# Design Automation - Migration Guide from V2 to V3 

[![Design-Automation](https://img.shields.io/badge/Design%20Automation-v3-lightblue.svg)](http://forge.autodesk.com/)

![Basic](https://img.shields.io/badge/Level-Basic-green.svg)
[![License](http://img.shields.io/:license-MIT-blue.svg)](http://opensource.org/licenses/MIT)

# Description

This is a quick transition guide for Design Automation from [V2](https://forge.autodesk.com/en/docs/design-automation/v2/developers_guide/overview/) to [V3](https://forge.autodesk.com/en/docs/design-automation/v3/developers_guide/overview/).

![](/thumbnail.png)

# Sections

## API Changes: :card_index:

This section maps the v2 endpoints with the new v3 endpoints.

- [AppBundles](apppackages.md)
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
 
# Further Reading

Documentation:

- [Design Automation](https://forge.autodesk.com/en/docs/design-automation/v3/developers_guide/overview/) (v3)

Tutorial:

- [Design Automation for AutoCAD tutorial](https://forge.autodesk.com/en/docs/design-automation/v3/tutorials/autocad/)

 
## License

This sample is licensed under the terms of the [MIT License](http://opensource.org/licenses/MIT). Please see the [LICENSE](LICENSE) file for full details.

## Written by

Madhukar Moogala [@galakar](https://twitter.com/galakar), [Forge Advocate](http://forge.autodesk.com)

