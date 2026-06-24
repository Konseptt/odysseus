## Bolt's Journal

## 2025-01-25 - Blocking bcrypt in FastAPI middleware
**Learning:** `bcrypt.checkpw` takes ~340ms to execute. When run directly inside Starlette's `BaseHTTPMiddleware` `async def dispatch`, it completely blocks the single-threaded asyncio event loop for all incoming requests.
**Action:** Always wrap CPU-bound cryptographic operations like `bcrypt.checkpw` in `asyncio.to_thread` when executing inside an `async` context to allow other asynchronous requests to process concurrently.
