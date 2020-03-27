# Migration Guide  V2 to V3 

A quick transition guide from forge design automation [V2](https://forge.autodesk.com/en/docs/design-automation/v2/developers_guide/overview/) to [V3](https://forge.autodesk.com/en/docs/design-automation/v3/developers_guide/overview/).

:zap: :zap: :zap:

Formerly known as the “AutoCAD I/O API”, the Design Automation API provides the ability to run scripts on your design files, leveraging the scale of the Forge Platform to automate repetitive tasks.

Index: :card_index:

- [activities](https://github.com/MadhukarMoogala/v2tov3/blob/master/activities.md)
- [appbundles](https://github.com/MadhukarMoogala/v2tov3/blob/master/workitems.md)
- [worktems](https://github.com/MadhukarMoogala/v2tov3/blob/master/apppackages.md)
- [engines](https://github.com/MadhukarMoogala/v2tov3/blob/master/engines.md)

  New  API Groups In V3 :new:

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

