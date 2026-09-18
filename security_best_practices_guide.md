# Security Best Practices Guide

## 1. Purpose

This guide provides centralized security best practices for developers and operators working with the Enterprise RAG Assistant. It focuses on authentication, role-based access control, secrets, data access, and secure deployment practices.

## 2. Security Areas

The project includes several security-sensitive areas:

- JWT-based authentication
- Role-based and department-based access control
- API authentication
- Environment variables and secrets
- Document and retrieval access
- Frontend token storage
- Production configuration

## 3. Authentication

The application uses JSON Web Tokens (JWT) for authentication.

### Best Practices

- Keep the JWT signing secret confidential.
- Do not commit secrets or API keys to the repository.
- Use environment variables for sensitive configuration.
- Use appropriately short token expiration periods for production.
- Reject invalid or expired tokens.
- Send authentication tokens only over HTTPS in production.

The backend creates JWTs using a secret key and an expiration time. Protected endpoints validate the token before processing authenticated requests.

## 4. Role-Based Access Control (RBAC)

The application uses roles and department scopes to control access.

Current roles include:

- `admin`
- `engineering`
- `hr`
- `operations`
- `support`

### Best Practices

- Apply authentication to every protected endpoint.
- Verify the user's role before allowing privileged operations.
- Restrict users to their permitted departments.
- Do not rely only on frontend controls for authorization.
- Perform authorization checks on the backend.

The repository currently uses `get_current_user()` for JWT validation and `require_admin()` for admin-only operations.

## 5. Department-Level Access

Users have a `departments_allowed` scope in their authentication information.

### Best Practices

- Validate requested departments against the authenticated user's allowed departments.
- Apply department filtering at the data retrieval layer.
- Never expose documents from departments the user is not authorized to access.
- Test access with users from different departments.

The repository resolves the user's allowed departments, but the README identifies an outstanding integration gap: the Qdrant department filter is not yet wired into the retriever. This should be addressed before relying on department-level retrieval isolation in production.

## 6. Secrets and Environment Variables

Sensitive values are configured through environment variables, including:

- `QDRANT_API_KEY`
- `GROQ_API_KEY`
- `SECRET_KEY`

### Best Practices

- Never commit API keys, passwords, or production secrets to Git.
- Keep `.env` files out of version control.
- Use secure secret-management mechanisms in production.
- Replace default or example secrets before deployment.
- Rotate exposed credentials immediately.

The repository currently documents `SECRET_KEY=change-me-for-production`; this value must not be used as a production secret.

## 7. API Security

The backend exposes authentication, chat, document, ingest, and feedback endpoints.

### Best Practices

- Require authentication for protected endpoints.
- Validate request data on the backend.
- Return appropriate authorization errors.
- Avoid exposing sensitive information in error responses.
- Use HTTPS for production API traffic.
- Apply appropriate rate limiting and monitoring in production.

## 8. Document and Data Protection

The application processes enterprise documents and stores document metadata, chunks, feedback, and chat logs.

### Best Practices

- Restrict document access according to user permissions.
- Avoid logging sensitive information unnecessarily.
- Protect database files and backups.
- Control access to Qdrant collections and API credentials.
- Remove sensitive test data before production deployment.

## 9. Frontend Security

The frontend currently stores the authentication token in `localStorage`.

### Best Practices

- Understand the risks of storing authentication tokens in browser storage.
- Consider secure `httpOnly` cookies or memory-only storage for production authentication.
- Do not store secrets or API keys in frontend source code.
- Do not rely on frontend UI restrictions as the primary security boundary.

The repository identifies token storage in `localStorage` as a known security consideration.

## 10. Production Configuration

Before deploying to production:

- [ ] Replace default secrets.
- [ ] Configure production environment variables securely.
- [ ] Use HTTPS.
- [ ] Remove development/mock configuration.
- [ ] Verify RBAC and department-level authorization.
- [ ] Review token expiration settings.
- [ ] Protect database and vector-store credentials.
- [ ] Review logging for sensitive information.
- [ ] Test unauthorized access scenarios.

## 11. Security Testing Checklist

Test the following scenarios:

- [ ] Unauthenticated users cannot access protected endpoints.
- [ ] Invalid or expired JWTs are rejected.
- [ ] Non-admin users cannot access admin-only upload functionality.
- [ ] Users cannot retrieve documents outside their permitted departments.
- [ ] Invalid department requests are rejected.
- [ ] API keys and secrets are not present in committed source code.
- [ ] Production builds do not use mock authentication/data.
- [ ] Sensitive information is not unnecessarily exposed in logs or responses.

## 12. Known Security Considerations

The repository documents the following security-related items that should be reviewed:

1. Department metadata filters are implemented but are not yet wired into the retrieval layer.
2. Mock mode is active by default and should be removed before a production build.
3. The JWT token is currently stored in `localStorage`.
4. `SECRET_KEY` has a development default and must be replaced for production.

These items should be tracked and addressed before production deployment.

## 13. Definition of Done

This guide is complete when developers and operators have a centralized reference covering:

- Authentication and JWT security
- RBAC and department access
- Secret management
- API security
- Document and data protection
- Frontend security considerations
- Production security checks
- Security testing checklist
