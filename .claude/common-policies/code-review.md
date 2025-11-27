# Code Review Standards

Universal code review principles for all projects.

## Core Philosophy

**Code is read more than run**: Optimize for the reader, not the writer. Code will be read hundreds of times but written once—clarity and readability always win.

**Catch what automated tools miss**: Look for subtle logic errors, unclear intent, missing edge cases, and violations of project conventions that linters can't detect.

**Maintainability focus**: Read code as if it will be maintained for a decade by someone who has never seen it.

## Review Priority

Prioritize ruthlessly in this order:

1. **Compliance violations** - HIPAA, PCI, regulatory requirements (must fix immediately)
2. **Security issues** - Authentication, authorization, data exposure (must fix)
3. **Correctness bugs** - Logic errors, edge cases, race conditions (must fix)
4. **Performance issues** - N+1 queries, missing indexes, blocking operations (should fix)
5. **Code quality** - Naming, structure, clarity (consider improving)

## Feedback Standards

**Specific file references**: Always include file paths and line numbers for issues found
- Example: `app/controllers/patients_controller.rb:42`

**Actionable feedback**: Explain what's wrong and suggest concrete improvements

**Context over criticism**: Explain why something matters (security, performance, maintainability)

## What to Look For

**Logic & Correctness**:
- Edge cases and boundary conditions
- Race conditions in concurrent code
- Proper error handling
- State management issues

**Security & Data Protection**:
- Authentication and authorization gaps
- Data exposure in logs, errors, URLs
- Input validation and sanitization
- Secure communication (HTTPS, encryption)

**Performance**:
- Database query efficiency (N+1 queries)
- Missing indexes on queried columns
- Blocking operations that should be async
- Inefficient algorithms or data structures

**Code Quality**:
- Clear naming (variables, functions, classes)
- Single Responsibility Principle
- Appropriate abstraction levels
- Self-documenting code vs. comments
