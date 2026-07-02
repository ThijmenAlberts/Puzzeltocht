## 2025-05-11 - [Middleware Database Queries]
**Learning:** Found an anti-pattern where a global middleware (`app.use`) performed a `Theme.findOne()` database query on every single request, including high-frequency API polling endpoints like `/api/director/pulse`.
**Action:** Always implement an in-memory cache (with a reasonable TTL, e.g., 5 minutes) for global configuration fetched from the database to prevent overwhelming the DB with redundant queries.

## 2024-05-15 - Optimize Read-Only Mongoose Queries
**Learning:** Mongoose queries without `.lean()` return heavy document objects with getters, setters, and change tracking overhead, which is unnecessary for read-only routes rendering views.
**Action:** Always append `.lean()` to Mongoose `find()` or `findById()` queries when the retrieved documents are only used for rendering or serialization, significantly improving performance and reducing memory usage.
