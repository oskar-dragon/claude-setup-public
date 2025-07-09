---
allowed-tools: Read, Write, Bash(fd:*), Bash(rg:*), Bash(gdate:*), Bash(jq:*), Task
description: Generate comprehensive API endpoint with framework detection, implementation, tests, and documentation
---

## Context

- Session ID: !`gdate +%s%N`
- Current directory: !`pwd`
- Project structure: !`fd . -t d -d 3 | head -20 || echo "No subdirectories found"`
- Technology stack: !`fd -e json -e toml -e go . | rg "(package\.json|go\.mod)" | head -5 || echo "No technology files detected"`
- Existing API files: !`fd "(api|controller|handler|route|endpoint)" . -t f | head -10 || echo "No API files found"`
- Framework configs: !`fd "(gin|express|hono)" . -t f | head -5 || echo "No framework configs found"`
- Database configs: !`fd "(database|db|migration|schema)" . -t f | head -5 || echo "No database configs found"`
- Test patterns: !`fd "\.(test|spec)\.(go|js|ts)$" . | head -5 || echo "No test files found"`
- Git status: !`git status --porcelain | head -5 || echo "Not a git repository"`
- Current branch: !`git branch --show-current 2>/dev/null || echo "No git repository"`

## Your Task

Generate comprehensive API endpoint for $ARGUMENTS using intelligent framework detection, parallel implementation, and extensive testing.

STEP 1: Framework Detection and Analysis

IF Java project detected (pom.xml/build.gradle):

- Analyze Spring Boot vs Quarkus patterns
- Check existing @RestController patterns
- Review Jackson/JSON configuration
  ELSE IF Rust project detected (Cargo.toml):
- Analyze Axum vs Actix-web usage patterns
- Check existing handler implementations
- Review serde configuration
  ELSE IF Go project detected (go.mod):
- Analyze ConnectRPC vs Gin/Echo patterns
- Check existing route definitions
- Review protobuf usage if ConnectRPC
  ELSE IF Node.js project detected (package.json):
- Analyze Express vs Fastify vs Hapi patterns
- Check existing middleware setup
- Review TypeScript configuration

STEP 2: API Design Phase (with Extended Thinking)

Think deeply about the optimal API design patterns for this specific endpoint:

- Consider RESTful vs gRPC vs GraphQL appropriateness
- Think harder about authentication and authorization requirements
- Analyze rate limiting and caching strategies
- Evaluate error handling and response patterns

Design decisions:

- HTTP method selection (GET, POST, PUT, DELETE, PATCH)
- RESTful URL path following project conventions
- Request parameters (path, query, body)
- Response schema and status codes
- Comprehensive error responses and edge cases
- Security considerations and input validation

STEP 3: Parallel Implementation Strategy

Use sub-agents for parallel development to optimize implementation time:

**Sub-Agent 1**: Core endpoint implementation
**Sub-Agent 2**: Comprehensive test suite generation
**Sub-Agent 3**: API documentation (OpenAPI/Swagger) generation
**Sub-Agent 4**: Database integration and migrations
**Sub-Agent 5**: Security and validation implementation

Implement endpoint based on detected framework:

**ConnectRPC (Go):**

```go
func (s *Server) Method(ctx context.Context,
    req *connect.Request[pb.Request]) (*connect.Response[pb.Response], error) {
    // Implementation
}
```

- Add comprehensive input validation and sanitization
- Implement business logic with proper separation of concerns
- Add structured error handling with proper HTTP status codes
- Include structured logging with correlation IDs
- Implement rate limiting and request throttling
- Add metrics and monitoring hooks

STEP 4: Security Implementation (Think deeply about security implications)

- Add robust authentication checks (JWT, OAuth2, API keys)
- Implement fine-grained authorization/permission checks
- Validate and sanitize all inputs (SQL injection, XSS prevention)
- Implement OWASP security headers
- Add CORS configuration with proper origin validation
- Implement request signing and verification if required
- Add security audit logging
- Configure rate limiting per user/IP

STEP 5: Comprehensive Test Generation

Generate extensive test suite covering all scenarios:

**Go (testing package):**

```go
func TestEndpoint(t *testing.T) {
    req := httptest.NewRequest("POST", "/api/v1/resource", body)
    w := httptest.NewRecorder()
    handler(w, req)
    assert.Equal(t, http.StatusOK, w.Code)
}
```

- Unit tests for all business logic
- Integration tests with database
- API contract tests (response schema validation)
- Security tests (auth bypass, injection attempts)
- Performance tests (load testing with k6 or Gatling)
- Edge cases and invalid input handling
- Error scenario testing (network failures, database issues)

STEP 6: Documentation Generation

- Generate OpenAPI/Swagger specification
- Create comprehensive request/response examples
- Document all error codes and troubleshooting
- Add rate limiting and quota information
- Document authentication and authorization requirements
- Provide Curl/HTTPie/client library examples
- Generate API changelog and versioning information

STEP 7: Database and Service Integration

Framework-specific database integration:

- **Go**: sqlx, GORM, Ent with connection pooling
- **Node.js**: Prisma

Implementation details:

- Implement repository/service pattern
- Generate database migrations (Flyway, migrate, sqlx)
- Configure connection pooling and health checks
- Add caching layer (DragonflyDB preferred over Redis)
- Consider event sourcing with RedPanda (preferred over Kafka)
- Implement database transaction management
- Add database monitoring and performance metrics

## Final Output

- Complete, production-ready endpoint implementation
- Comprehensive test suite with >90% coverage
- OpenAPI documentation with examples
- Database migrations and schema updates
- Security implementation with audit logging
- Performance optimizations and caching
- Client integration examples
- Deployment and monitoring configuration
