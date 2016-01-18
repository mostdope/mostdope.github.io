## How to customize errors using ASP.NET MVC ##

1. Add an **ErrorController** to your application, and add some methods if you need.
  For example methods are:
  
```csharp

public class ErrorController : Controller
{
    [HttpGet]
    [Route("error")]
    public ActionResult Index()
    {
        ViewBag.ErrorMessage = "Something goes wrong";
        return View("Error");
    }

    [HttpGet]
    [Route("error/NotFound")]
    public ActionResult NotFound()
    {
        ViewBag.ErrorMessage = "Nothing found here";
        return View("Error");
    }

    [HttpGet]
    [Route("error/Forbidden")]
    public ActionResult Forbidden()
    {
        ViewBag.ErrorMessage = "Access is denied";
        return View("Error");
    }
}
```
2. Open your **web.config** file and make some changes:
to ``` <system.web> ``` section
```xml
  <system.web>
    <customErrors mode="On" >
      <error statusCode="404" redirect="cborder/Error/NotFound"/>
      <error statusCode ="403" redirect="cborder/Error/Forbidden"/>
    </customErrors>
  </system.web>
```
and some changes in ``` <system.webServer> ``` :
```xml
<system.webServer>
  <httpErrors errorMode="Custom">
    <remove statusCode="403"/>
    <error statusCode="403" path="/error/forbidden" responseMode="Redirect"/>
  </httpErrors>
</system.webServer>
```
