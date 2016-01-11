Welcome to JSPTagEx!
===================

欢迎加入QQ群讨论（群号：431040030）

JSPTagEx的初衷在于简化Web开发，用更精简的代码实现一套类似SSH的后台框架，并提供一系列丰富的插件简化Web开发，***更少的依赖，更少的代码，更少的配置***，Enjoy It！

----------


基本功能
-------------
#### <i class="icon-file"></i> Maven Archetype

项目全程使用maven管理，根据不同业务需要拉取不同的maven archetype，目前包括：

 1. 纯Java服务；
 2. Web服务；
 3. Socket服务；

一键生成项目框架，按需补充业务代码即可。

#### <i class="icon-file"></i> MVC

编写Controller类只需继承BaseController即可，无需任何注解和配置，如下：

    public class TestController extends BaseController{
	    //match:webroot/restful/jsp
	    public String jsp()
	    {
		    return "/test.jsp";
	    }
	    //match:webroot/restful/ftl
	    public String ftl()
	    {
		    return "/test.ftl";
	    }
	    //match:webroot/restful/blog/xxxx
	    @URIAlias("blog/*")
	    public Blog getBlog()
	    {
		    Blog blog = Blog.me.findById(request.getAttribute("$1"),"*");
		    return blog;
	    }
    }

@URIAlias的注解可用于重命名URI，也可以在Class上使用这个注解。
	
#### <i class="icon-folder-open"></i> 数据库操作

支持直接JDBC操作也支持POJO风格的数据库操作，如下：

 1. 单条提取：Blog blog = Blog.me.findById("a","\*");//\*表示所有字段
 2. 新增记录：new Blog().set("id","1").set("title","博客标题").add();
 3. 保存记录：Blog.me.findById("a","1").set("title","修改后的标题").save();
 4. 删除记录：blog.deleteById("1");
> **事务操作** 
> DbUtils.tx(new ITx(){
	> @Override
	> public boolean run(Connection conn) throws Exception{
		>	  new Blog().set("id","1").set("title","test").add(conn);
		>    new Log().set("id","1").save(conn);	
	> }
> });


#### <i class="icon-pencil"></i> 数据集

后台支持三种数据集定义，分别是：SQL，JavaScript和Java类，满足不同所需；

 1. SQL：直接编写SQL语句，类似Mybatis的数据集定义；
 2. JavaScript：单纯SQL无法满足需求，需要根据条件组装SQL语句时，使用JavaScript语法；
 3. Java类：数据集的提取来自复杂的业务场景，直接集成AbsDataSetExec抽象类；

#### <i class="icon-trash"></i> AOP

基于注解，可拦截Controller类方法和全局拦截URL请求；

#### <i class="icon-hdd"></i> JSPTag Lib

提供丰富的标签库，使得Web开发更简单，并同时提供freemarker自定义标签；

 - 通用标签：choose-when-else标签，repeat循环标签等；
 - 数据集标签：sql,dataset,selectOne等标签；
 - 工具类标签：导出标签，权限判定标签等；


插件体系
-------------------

#### <i class="icon-refresh"></i> Connector插件

方便的连接sftp，qpid，activeMQ，LDAP等中间件，只需配置下XML并编写一下Listener类即可，无需依赖任何包。

#### <i class="icon-refresh"></i> 验证码插件

#### <i class="icon-refresh"></i> 上传服务插件

#### 等等,详见：http://nb.idbhost.com/jsptagex
