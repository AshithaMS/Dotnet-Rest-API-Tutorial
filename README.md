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

