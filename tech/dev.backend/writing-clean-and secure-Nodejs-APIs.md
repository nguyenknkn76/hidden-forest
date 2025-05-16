# Writing Clean, Secure Node.js APIs

## Structure Project Like a Pro
messy folder = messy code
a scalable structure:   
- `controllers`: business logic
- `routes`: API endpoints
- `services`: data and external API handling
- `middlewares`: logic for validation, authentication
- `models`: database schemas
- `utils`: helper functions 

> tip n trick: use folder structure that feels boring. but boring = predictable = easy to navigate.

## Validate All Incoming Data
Never trust client. Not even yourself if you're testing manually
- Use libraries (Joi, Zod, express-validator)
- Validate everything: headeres, query params, request bodies.
- Set clear rules for required fields, types, formats and limits.

## Always Handle Errors Properly
Crashing app b/c of a missing `try/catch`.
- Centralize error handling using middleware.
- Never leak stack traces or sesitive info to users
- Differentiate between client error (4xx) and server error (5xx).

## Secure API Like Bank Vault
Security isn't a nice-to-have. It's a must-have.
- Helmet.js: Secure HTTP headers.
- Ratelimiting: Prevent abuse (express-rate-limit)
- CORS: Strictly configure allowed origins.
- Authentication: Use JWT or OAuth2, not DIY tokens.
- Input Sanitization: Avoid SQL Injection/XSS (xss-clean) ?????

## Use Environment Variables (the right way)
## Version API
## Write Tests 
## Log Like a Detective
## Keep Dependencies Up-to-Date
## Document API
## Final Thoughts (authors)

> read more: https://dev.to/alisamir/writing-clean-secure-nodejs-apis-a-checklist-youll-actually-use-3loc 