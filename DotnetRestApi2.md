🧾 Common Return Types in .NET Web API

1. ✅ Ok() – HTTP 200
Returns a successful response with data.
```bash
return Ok(student);
```
2. 🚫 NotFound() – HTTP 404
Used when the requested resource is not found.
```bash
return NotFound();
```
Or with message:
```bash
return NotFound("Student not found");

```
3. 📤 CreatedAtAction() – HTTP 201
Used after creating a resource (like after POST). Returns the new resource URI + object.

```bash
return CreatedAtAction(nameof(GetStudent), new { id = student.Id }, student);
```
4. ♻️ NoContent() – HTTP 204
Used when the request was successful, but there is nothing to return. Often used with PUT/DELETE.
```bash
return NoContent();
```
5. ❌ BadRequest() – HTTP 400
Used for invalid or bad inputs.
```bash
return BadRequest("Invalid student ID");
```
Or with ModelState (automatic validation):
```bash
if (!ModelState.IsValid)
    return BadRequest(ModelState);
```
6. 🔐 Unauthorized() – HTTP 401
User is not authenticated (no/invalid token).
```bash
return Unauthorized();

```
7. ⛔ Forbid() – HTTP 403
User is authenticated but doesn’t have permission.
```bash
return Forbid();
```
8. 🧯 StatusCode(int code) – Custom status
Used when you want to return any custom status manually.
```bash
return StatusCode(500, "Server error occurred");

```
| Return Method       | HTTP Code | Use Case                      |
| ------------------- | --------- | ----------------------------- |
| `Ok(object)`        | 200       | Success with data             |
| `CreatedAtAction()` | 201       | Resource created              |
| `NoContent()`       | 204       | Success with no response body |
| `BadRequest()`      | 400       | Validation or bad input error |
| `Unauthorized()`    | 401       | Not logged in                 |
| `Forbid()`          | 403       | Access denied                 |
| `NotFound()`        | 404       | Resource not found            |
| `StatusCode(500)`   | 500       | Internal server error         |

✅ Example in a Controller Method
```bash
[HttpGet("{id}")]
public IActionResult GetStudent(int id)
{
    var student = StudentRepository.Students.FirstOrDefault(s => s.Id == id);
    if (student == null)
        return NotFound("Student with given ID not found");

    return Ok(student);
}

```

