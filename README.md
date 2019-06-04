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
- [Index file resource version](#index-file-resource-version)
- [Manifest resource version](#manifest-resource-version)
- [Web IDE project settings version](#web-ide-project-settings-version)

### Routing
- [Naming targets](#naming-targets)
- [Creating patterns](#creating-patterns)
- [Naming url parameters](#naming-url-parameters)

### Model-View-Controller
- [Using base controllers](#using-base-controllers)
- [Using parent controllers](#using-parent-controllers)
- [Exhausting models](#exhausting-models)
- [Reducing modules](#reducing-modules)
- [Reducing anonymous functions](#reducing-anonymous-functions)
- [Using i18n over text in code](#using-i18n-over-text-in-code)
- [Using correct odata types](#using-correct-odata-types)
- [Using correct CRUD operations](#using-correct-crud-operations)
- [Using createKey for CRUD operations](#using-createkey-for-crud-operations)
- [Using createEntry for create operations](#using-createentry-for-create-operations)

### Miscellaneous
- [Using SAPUI5 recommended eslint rules](#using-sapui5-recommended-eslint-rules)
- [customizing eslint rules](#customizing-eslint-rules)
- [documenting with jsdoc](#documenting-with-jsdoc)

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
GOOD:
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
GOOD:
```	
com.example.ztestapp
```

### **Keeping the project namespace descriptive or contain abbreviations of the app**
Keep namespaces readable and recognizable as much as possible. Use abbreviations to shorten the namespace. 

BAD:
```
com.1.0.1.app.test
```
GOOD:
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

## SAPUI5 Version

### **Index file resource version**
In actual projects, it is recommened to set a fix SAPUI5 version. This assures the supported libraries are compatible and consistent to your development setup. For stand alone application verify the `index.html` resource version.

![Index HTML](/images/index_html.png?raw=true)

### **Manifest resource version**
For launchpad ready applications, verify the version in the app descriptor file or `manifest.json`.

![Index HTML](/images/manifest_json.png?raw=true)

### **Web IDE project settings version**
Also verify the project settings in SAP Web IDE, to match your systems version.

![Index HTML](/images/project_settings.png?raw=true)

[Back to Table of Contents](#table-of-contents)

## Routing

### **Naming Targets**
Targets and routes should match view file to easily track the flow of the navigation. Also provide the following as minimal settings for targets:

- `viewLevel` - sets heirarchy to the application views.
- `transition` - the default transition behavior for the current target.
- `bypass` - fail safe target for unmatched routes.

### **Creating Patterns**
Route name should be descriptive by itself. Prefer *plural* form for routes if applicable.

BAD:
```
page1
itemDetail
```

GOOD:
```
home
itemDetails
```

### **Naming URL Parameters**
Routing parameters should be url safe, stay away from unsafe characters as parameters:

```
"{", "}", "|", "\", "^", "~", "[", "]", and "`"
```

Routing parametes should be *singular* form

BAD:
```
itemDetails/{objectIds}
orders/{orderItems}
```

GOOD:
```
itemDetails/{objectId}
orders/{orderId}
```

[Back to Table of Contents](#table-of-contents)

## Model-View-Controller

### **Using base controllers**
Move reusable functions to higher scope. The recommended base controller contents as follows:

- `getRouter`
- `getResourceBundle`
- `getModel`
- `setModel`
- `onNavBack`

### **Using parent controllers**
Enhance existing controllers by using them as parent controllers, but do take note:

>Note: The SAPUI5 controller extension concept does not use inheritance

### **Exhausting models**
Models allows you to write maintainable code. It also allows you to auto update control properties and bindings all at once. It also decouples the data to the presentation layer.

BAD:
```js
var oText = this.getView().byId("text-field");

oText.setText("hello");
oText.setTextAlign("End");
oText.setBusy(true);
// ... update only the oText control
```

GOOD:
```js
var oModel = this.getView().getModel();

oModel.setProperty("/message", "hello");
oModel.setProperty("/alignment", "End");
oModel.setProperty("/busy", true);
//... auto updates all controls with binding

```

### **Reducing modules**
Reduce response time and performance by using only what is needed by the application.

- Bootstraps  - preload modules in `manifest.json`, the ones used throughout the application.
- `constructor` and `onInit` -  dependencies loaded in the `sap.ui.define` of the controller.
- On-demand  - Inline `sap.ui.require`, for Dialogs and rarely used elements.

### **Reducing anonymous functions**
Prefer callbacks as separate function for readability and extensibility.

BAD:
```js
fnMyServiceCall: function() {
    var oModel = this.getView().getModel("view");
    oModel.read("/Orders", {
        success: function(oResult, oResponse){
            // do something
        },
        error: function(oError){
            // output error
        }
    })
}
```

GOOD:
```js
fnMyServiceCall: function() {
    var oModel = this.getView().getModel("view");
    oModel.read("/Orders", {
        success: this.fnSuccessCallback,
        error: this.fnErrorCallback
    })
},
fnSuccessCallback: function(oResult, oResponse){
    // do something
},
fnErrorCallback: function(oError){
    // output error
}
```

### **Using i18n over text in code**
BAD:
```js
onPressButton: function(){
	MessageToast.show("hey! hey! hey!");
}
```

GOOD:
```js
onPressButton: function(){
	MessageToast.show(this.getResourceBundle().getText("message"));
}
```

### **Using correct odata types**
Do not use `Edm.Strings` to represent the following, etc.:

- Date use `Edm.Date`
- Time use `Edm.Time`
- Currency use `Edm.Decimal`
- Flags (e.g. ABAP true, 'X') use `Edm.Boolean`

### **Using correct CRUD operations**
- Do not use `odata.create` to delete and override existing entry, use `odata.update`
- Do not use `odata.read`, `odata.create` for non-CRUD functionality like calculations and aggregations of results use `function import` instead.
- Do not use `odata.read` for `function import` use `callFunction`

```js
var oHandle = oModel.callFunction("/GetProductsByRating", {urlParameters: {rating:3}});
oHandle.contextCreated().then(function(oContext) {
      oView.setBindingContext(oContext);
});
```

### **Using createKey for CRUD operations**
Use `createKey` to generate collection URLs and to pre-validate against the `metadata` the existence of the collection.

BAD:
```js
myODataModel.update("/Orders(123)");
```

GOOD:
```js
var sPath = oModel.createKey("/Orders", {
  OrderId: 123, // your dynamic key value
});
oModel.update(sPath /*,...*/);
```

### **Using createEntry for create operations**
Use `createEntry` to instatiate new collection items for submission of entries.

```js
// create an entry of the Products collection with the specified properties and values
var oContext = oModel.createEntry("/Products", { 
		properties: { 
			Id:99, 
			Name:"Product", 
			Description:"new Product", 
			ReleaseDate:new Date(), 
			Price:"10.1", 
			Rating:1
		} 
	});

// binding against this entity
oForm.setBindingContext(oContext);
```

[Back to Table of Contents](#table-of-contents)