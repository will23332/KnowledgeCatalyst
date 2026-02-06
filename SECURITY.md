# Security Policy

## Reporting Security Issues

If you discover a security vulnerability in KnowledgeCatalyst, please report it to:
- **Email**: guglielmo.piacentini@dxc.com
- **Subject**: [SECURITY] KnowledgeCatalyst Vulnerability Report

Please do not report security vulnerabilities through public GitHub issues.

## Security Best Practices

### 1. Credentials Management

**IMPORTANT**: Never commit credentials to version control.

- ✅ **DO**: Use the `.env` file for credentials (already in `.gitignore`)
- ✅ **DO**: Set strong, unique passwords for Neo4j and API keys
- ✅ **DO**: Use different credentials for development and production
- ❌ **DON'T**: Commit `.env` file or hardcode credentials in source code
- ❌ **DON'T**: Use default passwords like "password123" in production

### 2. Neo4j Password Security

When setting up the project:

1. Copy `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```

2. **Change the default Neo4j password immediately**:
   ```bash
   # In .env file
   NEO4J_PASSWORD="your-very-secure-password-here"
   ```

3. Use a strong password with:
   - At least 16 characters
   - Mix of uppercase, lowercase, numbers, and symbols
   - No dictionary words

### 3. API Keys

- Store API keys in `.env` file only
- Never commit API keys to git
- Rotate API keys if accidentally exposed
- Use environment-specific keys (dev/staging/prod)

### 4. Production Deployment

For production deployments:

1. **Change all default passwords**
2. **Use HTTPS with valid SSL certificates**
3. **Configure firewall rules** to restrict access
4. **Enable Neo4j authentication** (don't disable it)
5. **Regularly update dependencies** for security patches
6. **Use secrets management** (e.g., AWS Secrets Manager, Azure Key Vault)
7. **Implement rate limiting** on API endpoints
8. **Configure CORS properly** for your domain
9. **Monitor logs** for suspicious activity

### 5. Docker Security

- Don't run containers as root user
- Scan images for vulnerabilities regularly
- Use specific image versions (not `latest`)
- Limit container resources (CPU, memory)
- Use Docker secrets for sensitive data in Swarm/Kubernetes

### 6. Network Security

- Use reverse proxy (Nginx/Traefik) with SSL/TLS
- Configure Neo4j to require encrypted connections
- Restrict database access to application network only
- Use VPC/private networks in cloud deployments

## Sensitive Data Handling

KnowledgeCatalyst processes potentially sensitive documents. To protect data:

1. **Data at Rest**:
   - Encrypt Neo4j data volumes
   - Use encrypted file storage (S3 with encryption, encrypted EBS volumes)

2. **Data in Transit**:
   - Use HTTPS for frontend
   - Use TLS for Neo4j connections (neo4j+s:// protocol)
   - Encrypt connections to LLM APIs (built-in with providers)

3. **Local LLM Option**:
   - Use Ollama for fully local operation (no data leaves your network)
   - Ideal for HIPAA, GDPR, or classified data requirements

## Vulnerability Disclosure

We take security seriously. If you report a vulnerability:

1. You will receive acknowledgment within 48 hours
2. We will investigate and provide a timeline for resolution
3. Once fixed, we will publicly disclose the vulnerability with credit to the reporter (if desired)
4. We will release a security advisory with mitigation steps

## Security Updates

- Security patches will be released as soon as possible
- Major security issues will be announced via GitHub Security Advisories
- Subscribe to GitHub notifications to stay informed

## Compliance Considerations

### HIPAA (Healthcare)
- Deploy on-premise or in HIPAA-compliant cloud environment
- Use Ollama for local LLM processing (no data sent to cloud APIs)
- Enable audit logging
- Encrypt all data at rest and in transit

### GDPR (EU Data Protection)
- Document data processing activities
- Implement data retention policies
- Enable right-to-erasure (delete document functions available)
- Process data locally when possible (Ollama)

### AGPL-3.0 License
- If you modify and deploy KnowledgeCatalyst as a network service, you must provide source code to users
- See LICENSE file for full terms

## Security Checklist for Production

Before going to production, verify:

- [ ] All default passwords changed
- [ ] `.env` file not committed to git
- [ ] HTTPS configured with valid certificate
- [ ] Firewall rules configured
- [ ] Neo4j authentication enabled
- [ ] Strong passwords for all services
- [ ] API keys rotated and stored securely
- [ ] CORS configured for your domain only
- [ ] Rate limiting enabled
- [ ] Logging and monitoring configured
- [ ] Regular backup schedule implemented
- [ ] Incident response plan documented
- [ ] Security updates scheduled

## Questions?

For security-related questions, contact: guglielmo.piacentini@dxc.com

---

**Last Updated**: February 2026
