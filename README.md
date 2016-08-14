# Saiku-ui-code-structure-analysis

1、Saiku简介

Saiku是一个轻量级的OLAP分析引擎，可以方便的扩展、嵌入和配置。Saiku通过REST API连接OLAP系统，利用其友好的界面为用户提供直观的分析数据的方式，它是基于backbone做的前端界面。

2、Saiku-ui结构分析

Saiku-ui的样式在css文件、图片在images文件、行为放在js(saiku)文件、内容index.html，server（node）代理服务器，其目录结构 
如下图所示：

![image](https://github.com/Fine0830/Saiku-UI-code-structure-analysis/blob/master/images/filepath.jpg)

2.1 index.html 
saiku采用jquery tmpl作为模板，通过模板ID在相应的view里面调用 
如：
<script type="text/x-jquery-tmpl" id="template-workspace">

在对应的在workspace.js里面的模板。

2.2 Saiku（全局对象）

Saiku-ui的设计模式采用单例模式，Saiku是全局对象，用来处理所有的应用程序状态，有如下的属性： 
1、Saiku.tabs：实现视图功能； 
2、Saiku.session：模型处理会话和身份验证； 
3、Saiku.routers：路由器页面片段的集合； 
4、Saiku.il8n：用户当前位置； 
5、Saiku.ui：提示UI； 
6、Saiku.events：自定义事件。

2.3模块功能介绍

模块代码结构脑图： 

![image](https://github.com/Fine0830/Saiku-UI-code-structure-analysis/blob/master/images/structure1.jpg)

1、Workspace：可视化区域；分别将Upgrade、WorkspaceDropZone、WorkspaceToolbar、QueryToolbar、Table、Chart、Query用new的方式加入到Workspace的属性和行为； 
2、Upgrade：获取提示信息； 
3、WorkspaceDropZone：设置工作区和其他交互，条件过滤； 
4、QueryToolbar：查询工具栏,和相关的可视化效果切换； 
5、Table：处理表格渲染出来的结果； 
6、Chart：处理显示相应图形渲染出来的结果； 
7、Query：工作区域里的请求模型； 
8、WarningModal：警告； 
9、DimensionList：维度列表控件的外观和行为； 
10、DateFilterModel：数据过滤模型； 
11、saikuTableRenderer：处理数据并将数据渲染成表格； 
12、saikuChartRenderer：处理数据并将数据可视化。

2.4 数据可视化分析

saiku可视化引用CCC_Charts(http://redmine.webdetails.org/projects/ccc/wiki/Chart_Samples_Links)，CCC_Charts是采用Protovis.js（D3的前身，同一作者）可视化库，其中sunburst没有封装在CCC里面，它是直接采用Protovis进行可视化，我们新增可视化库或者效果可采用sunburst的方法。 
在saikuChartRenderer对象里处理数据和可视化： 
switch_chart方法是对可视化效果的选择，新增的效果需要在此方法中定义； 
cccOptionsDefault方法是对CCC的配置； 
getQuickOptions对options的配置（chart类型、画布高度和宽度、颜色等参数）； 
define_chart是CCC的入口，通过此方法调用ccc里面的可视化效果； 
render_chart_element对图形的展示的动态设置，将方法中的animate初始值设为true，会给你额外的惊喜； 
process_data_tree后端传过来的数据进行数据的处理，方法较为复杂； 
sunburst是可视化的方法，采用Protovis。

3、总结 

![image](https://github.com/Fine0830/Saiku-UI-code-structure-analysis/blob/master/images/structure.jpg)
