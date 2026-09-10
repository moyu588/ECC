---
description: "评审 FastAPI 应用：架构、async 正确性、依赖注入、Pydantic schema、安全、性能与可测试性。"
---

# FastAPI Review

Invoke the `fastapi-reviewer` agent for a focused FastAPI review.

## Usage

```text
/fastapi-review [file-or-directory]
```

## Review Areas

- App factory, router boundaries, middleware, and exception handlers.
- Pydantic request and response schema separation.
- Dependency injection for database sessions, auth, pagination, and settings.
- Async database and external HTTP patterns.
- CORS, auth, rate limits, logging, and secret handling.
- OpenAPI metadata and documented response models.
- Test client setup and dependency overrides.

## Expected Output

```text
[SEVERITY] Short issue title
File: path/to/file.py:42
Issue: What is wrong and why it matters.
Fix: Concrete change to make.
```

## Related

- Agent: `fastapi-reviewer`
- Skill: `fastapi-patterns`
- Command: `/python-review`
- Skill: `security-scan`
