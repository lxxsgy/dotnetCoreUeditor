# UEditorNetCore  .net core 2.1
把durow/UEditorNetCore 升级到  .net core 2.1
原作者地址：https://github.com/durow/UEditorNetCore

百度在线编辑器UEditor在ASP.NET Core下的服务端，使用简单，易于扩展。
关于UEditorNetCore
百度在线编辑器UEditor在ASP.NET Core下的服务端，使用简单，易于扩展。
<br/>
相关文章：http://www.cnblogs.com/durow/p/6116393.html
<br/>
UEditor官网：http://ueditor.baidu.com/website/index.html
<br/>
UEditor源代码：https://github.com/fex-team/ueditor    

使用
1.在Startup.cs的ConfigureServices方法中添加UEditorNetCore服务
public void ConfigureServices(IServiceCollection services)
{
    //第一个参数为配置文件路径，默认为项目目录下config.json
    //第二个参数为是否缓存配置文件，默认false
    services.AddUEditorService()
    services.AddMvc();
}

2.添加Controller用于处理来自UEditor的请求
[Route("api/[controller]")] //配置路由
public class UEditorController : Controller
{
    private UEditorService ue;
    public UEditorController(UEditorService ue)
    {
        this.ue = ue;
    }
    public void Do()
    {
        ue.DoAction(HttpContext);
    }
}

3.修改前端配置文件ueditor.config.js
修改serverUrl为第2步Controller中配置的路由，使用例子中的路由按照以下配置：
serverUrl:"/api/UEditor"

4.修改服务端配置config.json
上传类的操作需要配置相应的PathFormat和Prefix，在示例中部署在web根目录，因此Prefix都设置为"/"。使用时要根据具体情况配置。 例如示例中图片上传的配置如下：
"imageUrlPrefix": "/", /* 图片访问路径前缀 */
"imagePathFormat": "upload/image/{yyyy}{mm}{dd}/{time}{rand:6}", 

5.添加javascript引用
<script type="text/javascript" charset="utf-8" src="~/lib/ueditor/ueditor.config.js"></script>
<script type="text/javascript" charset="utf-8" src="~/lib/ueditor/ueditor.all.min.js"> </script>
<script type="text/javascript" charset="utf-8" src="~/lib/ueditor/lang/zh-cn/zh-cn.js"></script>

