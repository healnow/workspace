# Security & Compliance Standards

Security and compliance requirements for healthcare and payment processing.

## HIPAA Compliance (Protected Health Information)

**PHI Definition**: Any individually identifiable health information including names, dates, contact info, medical records, health plan numbers, account numbers.

**Critical Rules**:
- **Never log PHI**: PHI must never appear in application logs, error messages, or debug output
- **Never expose in URLs**: PHI must not appear in URL parameters, paths, or query strings
- **Never expose in errors**: Stack traces and error messages must not contain PHI
- **Secure transmission**: All PHI transmission must be over HTTPS/TLS
- **Access controls**: Implement role-based access with audit trails
- **Session management**: Enforce session timeouts and secure session storage

**Examples of Violations**:
```ruby
# BAD - PHI in logs
logger.info "Patient #{patient.name} accessed record"

# GOOD - Use IDs only
logger.info "Patient ID #{patient.id} accessed record"
```

```javascript
// BAD - PHI in URL
fetch(`/api/patients?ssn=${patient.ssn}`)

// GOOD - PHI in request body
fetch('/api/patients', {
  method: 'POST',
  body: JSON.stringify({ patient_id: patient.id })
})
```

## PCI DSS Compliance (Payment Card Data)

**Cardholder Data**: Primary Account Number (PAN), cardholder name, expiration date, service code.

**Sensitive Authentication Data**: Full magnetic stripe, CAV2/CVC2/CVV2/CID codes, PINs.

**Critical Rules**:
- **Never store raw card numbers**: Always use tokenization (Stripe, etc.)
- **Never store CVV/CVC**: Security codes must never be persisted
- **Never log payment data**: Card numbers, CVV, full mag stripe data never in logs
- **Tokenization required**: Use payment processor tokenization for all card data
- **Secure transmission**: All payment data over HTTPS/TLS only
- **Minimize scope**: Reduce systems that handle cardholder data

**Examples of Violations**:
```javascript
// BAD - Storing raw card data
const payment = { cardNumber: '4242424242424242', cvv: '123' }
database.save(payment)

// GOOD - Use Stripe tokenization
const token = await stripe.createToken(cardElement)
database.save({ stripe_token: token.id })
```

## General Security

**Authentication & Authorization**:
- Implement proper authentication for all sensitive endpoints
- Use role-based access control (RBAC)
- Validate authorization on every request, not just UI

**Input Validation**:
- Validate and sanitize all user input
- Use parameterized queries to prevent SQL injection
- Escape output to prevent XSS attacks

**Secrets Management**:
- Never commit secrets, keys, or credentials to version control
- Use environment variables or secure credential stores
- Rotate credentials regularly

**Secure Communication**:
- All production traffic over HTTPS
- Use secure cookies (httpOnly, secure, sameSite)
- Implement proper CORS policies
