# SAPUI5 Best Practices
SAPUI5 Best Practices

A collection of SAPUI5 best practices learned from actual projects and implementations.

## Table of Contents

### Project Name and Namespaces
- [Following naming conventions](#following-naming-conventions)
- [Naming the project and namespace](#naming-the-project-and-namespace)
- [Keeping the project name and SAPUI5 ABAP repository name the same](#keeping-the-project-name-and-git-repository-name-similar)
- [Keeping the project name and git repository name similar](#keeping-the-project-name-and-git-repository-name-similar)
- [Following reverse-DNS for the project namespace](#following-reverse-dns-for-the-project-namespace)
- [Keeping the project namespace descriptive or contain abbreviations of the app](#keeping-the-project-namespace-descriptive-or-contain-abbreviations-of-the-app)

### Fiori Launchpad
- [Naming the catalog](#naming-the-catalog)
- [Naming the catalog group](#naming-the-catalog-group)
- [Naming semantic objects](#naming-semantic-objects)
- [Naming actions](#naming-actions)

### SAPUI5 Version
- [index file resource version](#index-file-resource-version)
- [manifest resource version](#manifest-resource-version)
- [Web IDE project settings version](#web-ide-project-settings-version)

### Routing
- [naming paths]()
- [creating patterns]()
- [naming url parameters]()

### Model-View-Controller
- [using base controllers]()
- [using parent controllers]()
- [exhausting models]()
- [reducing modules]()
- [reducing anonymous functions]()

### Miscellaneous
- [using SAPUI5 recommended eslint rules]()
- [customizing eslint rules]()
- [documenting with jsdoc]()

-----

## Project Name and Namespaces

### **Following naming conventions**
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

### **Naming the project and namespace**
Keep project name up to `15 characaters`. It will help you on your deployment to SAPUI5 ABAP Repository. SAPUI5 ABAP Repository has a limit of 15 characters for the new application name.

![Project Name Character Limit](/images/project_name_limit.png?raw=true)

BAD:
```
Z_TESTING_APPLICATION
```
Good:
```
Z_TESTAPP
```
### **Keeping the project name and SAPUI5 ABAP repository name the same**
Same project name and abap repository name, makes searching in `SICF` transaction easier.

![Project on SICF](/images/sicf_apps.png?raw=true)

### **Keeping the project name and git repository name similar**
SAP Web IDE Git only accepts lowercase alphanumeric characters and must not exceed `30 characters`.

![Git Repository Name](/images/git_repo.png?raw=true)

### **Following reverse-DNS for the project namespace**
[Reverse-DNS](https://en.wikipedia.org/wiki/Reverse_domain_name_notation) identify resources quickly. It helps avoid naming collision and duplicates. It also organizes the applications in a modular manner. Also, try to keep the project namespace to `3 segments`.

BAD:
```
my.awesome.app.com
```
Good:
```	
com.example.ztestapp
```

### **Keeping the project namespace descriptive or contain abbreviations of the app**
Keep namespaces readable and recognizable as much as possible. Use abbreviations to shorten the namespace. 

BAD:
```
com.1.0.1.app.test
```
Good:
```	
com.example.ztestapp
com.mycompany.timesheet
```

[Back to Table of Contents](#table-of-contents)

## Fiori Launchpad

### **Naming the catalog**
Catalog should be easy to be identified via name

FORMAT:
```
Z_<3-character SAP module>_C_<catalog name>
```

SAMPLE:
```
Z_HCM_C_ESS
```

### **Naming the catalog group**
Similar to catalog, should be identifiable via name

FORMAT:
```
Z_<3-character SAP module>_G_<catalog name>
```

SAMPLE:
```
Z_HCM_G_ESS
```

### **Naming semantic objects**
Semantic objects must represent entities and not actions.

> Represents a business entity such as a customer, a sales order, or a product. Using semantic objects, you can bundle applications that reflect a specific scenario. They allow you to refer to objects in a standardized way, abstracting from concrete implementations of these objects.<br/>You can either use semantic objects shipped by SAP, or create new semantic objects.

BAD:
```
#ZHCM_EXT_APP
#zHcmCreate
```

GOOD:
```
#SalesOrder
```
### **Naming actions**
Actions are more specific to what the task being performed by the user.

BAD:
```
salesOrderActive
timesheetError
```

GOOD:
```
displayFactSheet
manageTimesheet
```

COMPLETE FORMAT:
```
<semantic object>-<action>?<semantic object parameter>=<value1>
```

[Back to Table of Contents](#table-of-contents)

### **Index file resource version**
In actual projects, it is recommened to set a fix SAPUI5 version. This assures the supported libraries are compatible and consistent to your development setup. For stand alone application verify the `index.html` resource version.

![Index HTML](/images/index_html.png?raw=true)

### **Manifest resource version**
For launchpad ready applications, verify the version in the app descriptor file or `manifest.json`.

![Index HTML](/images/manifest_json.png?raw=true)

### **Web IDE project settings version***
Also verify the project settings in SAP Web IDE, to match your systems version.

![Index HTML](/images/project_settings.png?raw=true)

[Back to Table of Contents](#table-of-contents)