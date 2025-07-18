🧾 **Specialized Return Types in ASP.NET Core Web API**

1. 📝**ContentResult** 
Used to return plain text, HTML, or any string content.
```bash
[HttpGet("text")]
public ContentResult GetText()
{
    return Content("This is plain text response", "text/plain");
}

```
- Content(string content, string contentType, Encoding encoding)

- Example: text/html, text/plain, text/xml
 
2. 📄 **FileResult**  
   Used to return files (PDF, images, CSV, etc.) from API.
     - FileContentResult  
       Return a byte array as a file:
       ```bash
        [HttpGet("download")]
        public FileResult DownloadFile()
        {
            var bytes = System.IO.File.ReadAllBytes("Files/sample.pdf");
            return File(bytes, "application/pdf", "sample.pdf");
        }
       ```
       
    - PhysicalFileResult  
    Return a file from the server's physical path:
      ```bash
        [HttpGet("get-file")]
      public IActionResult GetFile()
      {
          return PhysicalFile("C:\\Reports\\report.csv", "text/csv", "report.csv");
      }
      ```
      
   - VirtualFileResult  
     If using wwwroot or static file folders:
        ```bash
        return File("~/wwwroot/sample.txt", "text/plain", "sample.txt");
        ```
3. 📦 **JsonResult**  
Returns JSON manually (rarely used now since Ok() already returns JSON).
  ```bash
  [HttpGet("json")]
public JsonResult GetJson()
{
    var data = new { Name = "Ashitha", Role = "Developer" };
    return new JsonResult(data);
}
  ```
Prefer return Ok(object) in most cases. JsonResult is useful for controlling formatting options.  

4. 🔄 **RedirectResult / RedirectToActionResult**  
Redirects to another route or URL.
  ```bash
public IActionResult RedirectExample()
{
    return Redirect("https://example.com");
}
  ```
  ```bash
public IActionResult RedirectToOtherAction()
{
    return RedirectToAction("GetStudents");
}

  ```

5. 🚫 **StatusCodeResult**  
Return any specific status code without body.

  ```bash
return StatusCode(418); 

  ```

| Type               | When to Use                                         |
| ------------------ | --------------------------------------------------- |
| `ContentResult`    | Return plain string or HTML                         |
| `FileResult`       | Download files, images, reports                     |
| `JsonResult`       | Explicit JSON response (e.g., custom serialization) |
| `RedirectResult`   | Redirect user to another route or external site     |
| `StatusCodeResult` | For rare/custom status codes                        |

✅ **Quick Example Controller**

 ```bash
[ApiController]
[Route("api/demo")]
public class DemoController : ControllerBase
{
    [HttpGet("plain")]
    public ContentResult GetText() => Content("Plain Text", "text/plain");

    [HttpGet("json")]
    public JsonResult GetJson() => new JsonResult(new { message = "Hello" });

    [HttpGet("file")]
    public FileResult GetPdf()
    {
        var fileBytes = System.IO.File.ReadAllBytes("Files/sample.pdf");
        return File(fileBytes, "application/pdf", "sample.pdf");
    }

    [HttpGet("redirect")]
    public IActionResult GoToGoogle() => Redirect("https://google.com");

    [HttpGet("status")]
    public IActionResult GetCustomStatus() => StatusCode(418, "I’m a teapot");
}

 ```
