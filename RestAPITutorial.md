📘 Notes to Create .NET REST API in C#
1. ✅ Prerequisites
-	Visual Studio 2022+ or VS Code with C# plugin
-	.NET SDK (.NET 6 or 7 recommended)
-	Basic knowledge of C# and OOP
________________________________________
2. 🌐 What is a REST API?
-	REST stands for Representational State Transfer
-	REST APIs use HTTP methods like GET, POST, PUT, DELETE
-	Used to communicate between client and server over the web
________________________________________
3. 🛠️ Create a .NET Web API Project
Using Visual Studio:
-	File > New > Project
-	Choose ASP.NET Core Web API
-	Name your project (e.g., StudentAPI)
-	Select .NET 6 or later
-	Check Use controllers & uncheck Enable OpenAPI (optional)
Using CLI:
```bash

dotnet new webapi -n StudentAPI
cd StudentAPI
dotnet run
```
________________________________________
4. 📁 Project Structure Overview

```bash
StudentAPI/
├── Controllers/
│   └── WeatherForecastController.cs (delete or edit)
├── Program.cs
├── Startup.cs (if using older versions)
├── Properties/
├── appsettings.json
```
________________________________________
5. 🧱 Create a Model (Entity)

```bash
// Models/Student.cs
public class Student
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
}
```
________________________________________
6. 🧠 Create a Fake Repository (In-memory storage)

```bash
// Data/StudentRepository.cs
public static class StudentRepository
{
    public static List<Student> Students = new List<Student>
    {
        new Student { Id = 1, Name = "John", Age = 20 },
        new Student { Id = 2, Name = "Emma", Age = 22 }
    };
}
```
________________________________________
7. 🧾 Create a Controller

```bash
// Controllers/StudentController.cs
using Microsoft.AspNetCore.Mvc;

[ApiController]
[Route("api/[controller]")]
public class StudentController : ControllerBase
{
    [HttpGet]
    public ActionResult<IEnumerable<Student>> GetStudents()
    {
        return Ok(StudentRepository.Students);
    }

    [HttpGet("{id}")]
    public ActionResult<Student> GetStudent(int id)
    {
        var student = StudentRepository.Students.FirstOrDefault(s => s.Id == id);
        if (student == null) return NotFound();
        return Ok(student);
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
```
________________________________________
8. 🔍 Test the API

•	Run the project

•	Use Swagger UI or Postman

o	GET /api/student

o	POST /api/student

o	PUT /api/student/{id}

o	DELETE /api/student/{id}

________________________________________
9. ⚙️ Enable Swagger (Optional for testing)
Add this to Program.cs:

```bash
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

app.UseSwagger();
app.UseSwaggerUI();
```
________________________________________
10. 📌 Tips for Freshers
-	Practice by creating CRUD for multiple entities
-	Use Postman to understand API requests/responses

