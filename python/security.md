---
globs:
  - "**/*.py"
  - "**/*.pyi"
---

# Python Security

## Secrets

- Use `load_dotenv()` for local `.env` loading when needed.
- Read required secrets from environment variables with fail-fast access such as `os.environ["OPENAI_API_KEY"]`.
