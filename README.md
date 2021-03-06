## Test A-CAD project.
### Main goal: 
`Implement functionality analogue to AutoCAD like tools`.

### Start project: 
To start a project initialize import of project or open pom.xml as project.
Used IDEA: IntelliJ 2017 Ultimate version (with web-app support).
Requirement: JAVA 8, embedded tomcat is used from the box with spring boot configured application.
Deployed web-application is available after start via: 
[http://localhost:8888/](http://localhost:8888/)
 
### Input data:
From start based project contains mocked data of schema-1 for draw, manipulation and properties 
representation. 
Each `Schema` object contains property for grid drawing (to see more details about
properties, check comments @see `Schema.java`).
To start draw schema grid, select schema object using: `/api/getSchema/{id}` call 
(@see `MainCadController.java`). Main properties of grid: `sizeX`, `sizeY`, `gridStepX`, `gridStepY`,
`disableDeleting`.
**All objects properties should be shown in a right-side panel with button save and editable fields related 
to each property. If no object was selected, by default show Schema properties, as it is 'unselectable'.**
To save Schema object use `/api/saveSchema/{id}` call, same pattern for manipulation with data is used for all other
objects:
- BuildingArea (@see `BuildingArea.java`), rectangle that represents limited space for placement of other objects.
- Box (@see `Box.java`), rectangle that represents container of {@see `InsideBox`}es, 
placed in scope of {@link BuildingArea}. Depends on frontSide (@see `FrontSide.java`), from which box is entered, and to which its inside
 structure is aligned. Inside structure is drawn as greed based on `rows` and `cols`, always in equal proportions.
 I.E. here is [IMG](https://2r4s9p1yi1fa2jd7j43zph8r-wpengine.netdna-ssl.com/files/2017/10/grid-numbers.png):<br>
 `3 columns and 2 rows if frontSide is TOP or BOTTOM.` <br>
 `2 columns and 3 rows if frontSide is RIGHT or LEFT.`
  <br>In each of such inside rectangle could be placed InsideBox. 
- InsideBox (@see `InsideBox.java`), specific object, which represent small box, which exists always and only
inside of {@see `Box`}.
- Network (@see `Network.java`) - object, which represent network, which contains {@see `StepPoint`}s 
linked by {@see `ConnectedLine`}s between each other. Also include property which define type of 
{@see `Walker.java`}.
- StepPoint (@see `StepPoint.java`) - object, which represents point, related to {@see `Network`}, 
which usually is part of {@see `ConnectedLine`}.
- ConnectedLine (@see `ConnectedLine.java`) - object, which represent directed or not line, with start and end 
{@see `StepPoint`}.
<br><br>To retrieve any objects by schema Id use GET request call like `/api/get{EntityName}s/{id}`, where {EntityName} is
Box, ConnectedLine, StepPoint, Network, ... etc. and {id} - is id of schema, to which such objects are related.
<br><br>To get single object by schema Id and its id use GET request call like `/api/get{EntityName}/{schemaId}/{id}`. 
<br><br>To save any object use POST request call like: `/api/save{EntityName}/{id}`, where id is schemaId. Such call could
be used in both cases, whether we store new or update existing entity.

### TODO steps.
1) From start point `home.jsp` we open page `editor.jsp` via 2 buttons to open schema #1 or #2. Currently 
available only 1-st schema (with id = 1). When we enter editor of such schema, we need to get 
{@see `Schema`} object and based on it property draw grid. On top should be panel with possible actions 
(here is just panel, filling in next steps).
<br>Left side panel list top level objects and include buttons to add new objects (here is just panel, filling in next steps).
<br>Right side panel includes property of selected object (TODO in step 2, here is currently just a panel).
2) Add support of Schema properties representation at right side panel, makes them editable and with possibility to 
store updated properties, (with possibility to apply same logic for any other object).
3) Add support and drawing of objects: Building Areas and Boxes (check entities package and JavaDoc to classes for more information).
Be sure that right side panel properties are changeable, and changes stored if save button is pressed, or reverted if object 
is deselected. All changes that influence on position \ size \ color should be visible during changes.
4) Add support and drawing of objects: Networks, StepPoints, Connected Lines 
(check entities package and JavaDoc to classes for more information). Same manipulations with properties 
support as in 3 point.
5) Add support of adding new objects and saving them with changed properties to back-end.
6) Add possibility to move \ rotate objects, linked objects together.
7) Add support of InsideBoxes.

TODO: ....