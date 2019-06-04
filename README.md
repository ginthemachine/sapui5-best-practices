# SAPUI5 Best Practices
SAPUI5 Best Practices

A collection of SAPUI5 best practices learned from actual projects and implementations.

## Table of Contents
### Project Name and Namespaces
- [Following naming conventions](#following-naming-conventions)
- [Naming the project and namespace](#namespace)
- [Following reverse-DNS for the project namespace]()
- [Keeping the project name and SAPUI5 ABAP repository name the same]()
- [Keeping the project name and git repository name similar]()
- [Keeping the project namespace descriptive or contain abbreviations of the app]()

### Fiori Launchpad
- [Naming the catalog]()
- [Naming the catalog group]()
- [Naming semantic objects]()
- [Naming actions]()

### SAPUI5 Version
- [index.html resource version]()
- [manifest.json resource version]()
- [Web IDE project settings version]()

### Model-View-Controller
- [using base controllers]()
- [using parent controllers]()
- [exhausting models]()
- [reducing modules]()
- [reducing anonymous functions]()

### Routing
- [naming paths]()
- [creating patterns]()
- [naming url parameters]()

### Miscellaneous
- [using SAPUI5 recommended eslint rules]()
- [customizing eslint rules]()
- [documenting with jsdoc]()

#### **Following naming conventions**
Use hungarian notation for naming variable name and object properties:

Sample|Type
------------ | ------------- 
sId | string
oDomRef | object
$DomRef	| jQuery object
iCount | int
mParameters | map / assoc. array
aEntries | array
dToday | date
fDecimal | float
bEnabled | boolean
rPattern | RegExp
fnFunction | function
vVariant | variant types

You can also refer to this in-depth naming convention as a reference. `(TO FOLLOW)`
#### **Naming the project and namespace**
Keep project name up to `15 characaters`. It will help you on your deployment to SAPUI5 ABAP Repository. SAPUI5 ABAP Repository has a limit of 15 characters for the new application name.

![SAPUI5 Best Practice](/images/project_name_limit.png?raw=true)

BAD:
```
Z_TEST_CUSTOM_APPLICATION
```
Good:
```
Z_TEST_CUST_APP
```
