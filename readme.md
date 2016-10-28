Saiku-ui-code-structure-analysis

1、Saiku introduce

 Saiku is a lightweight OLAP analysis engine that can be easily expanded, embedded, and configured. Saiku through API REST connected to the OLAP system, the use of its friendly interface to provide users with intuitive analysis of the data, it is based on the MV* backbone.js framework to achieve front-end functions

2、Saiku-ui code structure analysis

Saiku-ui style in the CSS files, pictures in the images files, acts on the JS (saiku) file, the contents of server, 
index.html (node) proxy server, the directory structure as shown below:

![image](https://github.com/Fine0830/Saiku-UI-code-structure-analysis/blob/master/images/filepath.jpg)

2.1、index.html 

Saiku use tmpl jQuery as a template, the template through the corresponding ID inside the view call 
in the corresponding template in the workspace.js.
```
<script type="text/x-jquery-tmpl" id="template-workspace">
```
2.2、Saiku（global Object）

Saiku-ui design model uses a single case model, Saiku is a global object, used to handle all the application status, 
there are the following attributes:
1、Saiku.tabs：View which handles tabs； 
2、Saiku.session：Model which handles session and authentication； 
3、Saiku.routers：Collection of routers for page fragments； 
4、Saiku.il8n：The user's current locale； 
5、Saiku.ui：Convenience functions for blocking the UI； 
6、Saiku.events：Global event bus.

2.3 Modules introduce

modules structure brain map
![image](https://github.com/Fine0830/Saiku-UI-code-structure-analysis/blob/master/images/structure1.jpg)

1、Workspace：the analysis workspace；Upgrade、WorkspaceDropZone、WorkspaceToolbar、QueryToolbar、Table、Chart、Query are Workspace's behaviour or property； 
2、Upgrade：The global toolbar； 
3、WorkspaceDropZone：Sets up workspace drop zones for DnD and other interaction； 
4、QueryToolbar：The query toolbar, and associated actions； 
5、Table：Class which handles table rendering of resultsets； 
6、Chart：Renders a chart for each workspace； 
7、Query：Workspace query； 
8、WarningModal：The "about us" dialog； 
9、DimensionList：This is where drag and drop lives； 
10、DateFilterModel：Dialog for date filter； 
11、saikuTableRenderer：data process and charts render； 
12、saikuChartRenderer：data process and table render。

2.4 Data visualization

Saiku use CCC_Chart(http://redmine.webdetails.org/projects/ccc/wiki/Chart_Samples_Links) plugin to visualize data,CCC_Chart use protovis 
visualization library.SaikuChartRenderer object proccess data and render chart,switch_chart function switch charts,
if you add charts,you need to add paramter;cccOptionsDefault function is default optimised ；getQuickOptions configuration on the options 
(chart type, height and width of the canvas, color and other parameters); define_chart function is the entrance of CCC plugin, 
through the visual effect of the call the CCC method inside; dynamic setting render_chart_element graphics display, 
the animate method in the initial value is set to true, will give you an extra surprise; the process_data_tree backend data transmission over the data processing, 
the method is complicated; Sunburst is the visual method, using Protovis. 

3、Summary

![image](https://github.com/Fine0830/Saiku-UI-code-structure-analysis/blob/master/images/structure.jpg)
