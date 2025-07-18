# 🌐 Beginner's Guide to Creating a .NET REST API with C#

This project provides a complete starter guide for **freshers** looking to build their first **.NET Web API** using **C#**. It includes API basics, CRUD implementation, and various return types including `Ok`, `NotFound`, `ContentResult`, and `FileResult`.

---

## ✅ Prerequisites

- [.NET 6 or 7 SDK](https://dotnet.microsoft.com/en-us/download)
- [Visual Studio 2022+](https://visualstudio.microsoft.com/) or [VS Code](https://code.visualstudio.com/) with C# plugin
- Basic C# and OOP knowledge

---

## 🛠️ Project Setup

### Using CLI

```bash
dotnet new webapi -n StudentAPI
cd StudentAPI
dotnet run
```

Using Visual Studio
File → New → Project → ASP.NET Core Web API

Choose .NET 6 or later

Name your project (e.g., StudentAPI)

Check "Use Controllers" (optional: disable OpenAPI)

📁 Folder Structure
StudentAPI/
├── Controllers/
│   └── StudentController.cs
├── Models/
│   └── Student.cs
├── Data/
│   └── StudentRepository.cs
├── Program.cs
├── appsettings.json

🧱 Define the Model
// Models/Student.cs
public class Student
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
}
📦 In-Memory Repository
// Data/StudentRepository.cs
public static class StudentRepository
{
    public static List<Student> Students = new List<Student>
    {
        new Student { Id = 1, Name = "John", Age = 20 },
        new Student { Id = 2, Name = "Emma", Age = 22 }
    };
}
🧾 Student Controller with CRUD APIs
// Controllers/StudentController.cs
[ApiController]
[Route("api/[controller]")]
public class StudentController : ControllerBase
{
    [HttpGet]
    public ActionResult<IEnumerable<Student>> GetStudents() => Ok(StudentRepository.Students);

    [HttpGet("{id}")]
    public ActionResult<Student> GetStudent(int id)
    {
        var student = StudentRepository.Students.FirstOrDefault(s => s.Id == id);
        return student == null ? NotFound("Student not found") : Ok(student);
    }

    [HttpPost]
    public ActionResult AddStudent(Student student)
    {
        StudentRepository.Students.Add(student);
        return CreatedAtAction(nameof(GetStudent), new { id = student.Id }, student);
    }

    [HttpPut("{id}")]
    public ActionResult UpdateStudent(int id, Student student)
    {
        var existing = StudentRepository.Students.FirstOrDefault(s => s.Id == id);
        if (existing == null) return NotFound();
        existing.Name = student.Name;
        existing.Age = student.Age;
        return NoContent();
    }

    [HttpDelete("{id}")]
    public ActionResult DeleteStudent(int id)
    {
        var student = StudentRepository.Students.FirstOrDefault(s => s.Id == id);
        if (student == null) return NotFound();
        StudentRepository.Students.Remove(student);
        return NoContent();
    }
}
🧾 Common Return Types
| Return Method       | HTTP Code | Description                   |
| ------------------- | --------- | ----------------------------- |
| `Ok(object)`        | 200       | Successful response with data |
| `CreatedAtAction()` | 201       | Resource created              |
| `NoContent()`       | 204       | Success with no response body |
| `BadRequest()`      | 400       | Invalid input                 |
| `Unauthorized()`    | 401       | No authentication             |
| `Forbid()`          | 403       | Forbidden access              |
| `NotFound()`        | 404       | Resource not found            |
| `StatusCode(500)`   | 500       | Internal server error         |
🧰 Advanced Return Types

ContentResult - Plain Text
return Content("Plain text message", "text/plain");
FileResult - Return Files
var bytes = System.IO.File.ReadAllBytes("Files/sample.pdf");
return File(bytes, "application/pdf", "sample.pdf");
JsonResult - Manual JSON Response
return new JsonResult(new { name = "Ashitha", role = "Developer" });
RedirectResult - URL Redirection
return Redirect("https://example.com");
🔍 Test with Swagger or Postman
Run the API

Open Swagger UI at: https://localhost:<port>/swagger

Or test with Postman:

GET /api/student

POST /api/student

PUT /api/student/{id}

DELETE /api/student/{id}

