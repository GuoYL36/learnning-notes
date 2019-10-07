maven和idea基础


groupid和artifactid被统称为“坐标”，是为了保证项目唯一性而提出的，如果你要把你项目弄到maven本地仓库去，你想要找到你的项目就必须根据这两个id去查找。

groupId一般分为多个段，这里我只说两段，第一段为域，第二段为公司名称。域又分为org、com、cn等等许多，其中org为非营利组织，com为商业组织。举个apache公司的tomcat项目例子：这个项目的groupId是org.apache，它的域是org（因为tomcat是非营利项目），公司名称是apache，artigactId是tomcat。

比如我创建一个项目，我一般会将groupId设置为cn.snowin，cn表示域为中国，snowin是我个人姓名缩写，artifactId设置为testProj，表示你这个项目的名称是testProj，依照这个设置，你的包结构最好是cn.snowin.testProj打头的，如果有个StudentDao，它的全路径就是cn.snowin.testProj.dao.StudentDao。


Maven Projects中
	Lifecycle表示maven生命周期，通过maven自带的命令来完成操作。
	Plugins：依赖项目的pom文件中所配置的插件来完成操作。


项目必须安装后再执行tomcat，不然会找不到。

对于pom中没有配置的插件，执行plugins中tomcat7里面的run肯定会报错。如果是这样，可以先对点击每个项目的Lifecycle中maven的命令(Install)进行安装，然后再运行tomcat。


Tomcat插件使用
第一种方式
	在子项目中配置tomcat插件要求所有的聚合工程必须进行安装。如果项目A没有被其他项目依赖，可以先对项目A中lifecycle执行Install命令进行安装，然后对其他项目进行一样的操作(每个项目下都会生成一个target文件)，安装完后就可以执行tomcat-run了。

第二种方式
	在父项目中配置tomcat插件不要求所有的聚合工程必须安装。将tomcat插件放在副工程(manage)当中的pom文件中进行配置，这样做的好处是不需要在每个项目中都安装。首先在manage项目里的pom文件配置tomcat插件，将所有项目里面的jar全部清除(点击每个项目的lifecycle下的clean，会清除掉各个项目的target文件)，然后点击manage项目的plugins中tomcat-run就可以了。