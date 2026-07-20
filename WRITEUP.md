FIX 1 – SQL Injection (Login)
Problem:
The login query put user input directly into the SQL statement, which allowed SQL injection.
Payload:
curator' --
Fix:
I changed the query to use parameterized queries. This allows the the database to use the input as data instead of SQL code. The only issue is people can still make weak passwords.

FIX 2 – SQL Injection (Search)
Problem:
The search query allowed SQL injection through the search box and sort option.
Payload:
' UNION SELECT 0, username, password, 'users' FROM users --
Fix:
I used parameterized queries and an allow-list for the order by column. The User input cannot change the SQL query.

FIX 3 – Reflected XSS
Problem:
The search term was displayed without being encoded.
Payload:
<img src=x onerror=alert("XSS")>
Fix:
I used escapeHtml() before displaying the search term. This allows the browser to show the input as text instead of running it.

FIX 4 – Stored and DOM XSS
Problem:
Comments and the shared note could run JavaScript.
Payload:
<img src=x onerror="alert('xss')">
Fix:
I encoded comments with escapeHtml() and replaced innerHTML with textContent. This allows The to treat the input as plain text. This is only a temporary fix.

FIX 5 – Cookie Flags and CSP
Problem:
The session cookie was missing security flags, and there was no Content Security Policy.
Payload:
I used the provided exploit script to check the cookie and headers.
Fix:
I added HttpOnly, SameSite=Strict, and a Content Security Policy. This helps protect the session cookie and blocks many injected scripts.