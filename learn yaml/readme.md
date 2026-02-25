---
title: "Learn Complete YAML"
description: "A comprehensive developer's guide to YAML - from basics to advanced techniques"
icon: "file-code"
---

# 💡 YAML: A Developer's Guide

<Note>
*"Like managing a secure banking system, writing YAML is all about precision, structure, and keeping every detail in its proper place."*
</Note>

## 📋 Table of Contents

<CardGroup cols={2}>
  <Card title="What is YAML?" icon="circle-question" href="#what-is-yaml">
    Introduction and basics
  </Card>
  <Card title="Basic Syntax" icon="code" href="#basic-syntax">
    Key-value pairs and comments
  </Card>
  <Card title="Data Types" icon="database" href="#data-types">
    Strings, numbers, booleans
  </Card>
  <Card title="Collections" icon="layer-group" href="#collections">
    Lists and dictionaries
  </Card>
  <Card title="Advanced Features" icon="wand-magic-sparkles" href="#advanced-features">
    Anchors, aliases, and more
  </Card>
  <Card title="Common Pitfalls" icon="triangle-exclamation" href="#common-pitfalls">
    Mistakes to avoid
  </Card>
  <Card title="Real-World Examples" icon="rocket" href="#real-world-examples">
    CI/CD, Docker, Kubernetes
  </Card>
  <Card title="Best Practices" icon="star" href="#best-practices">
    Tips and tools
  </Card>
</CardGroup>

---

## What is YAML?

**YAML** stands for "YAML Ain't Markup Language" (recursive acronym)

<CardGroup cols={2}>
  <Card icon="book-open">
    **Human-readable** data serialization format
  </Card>
  <Card icon="gear">
    Commonly used for **configuration files**
  </Card>
  <Card icon="code">
    **Superset of JSON** - cleaner syntax
  </Card>
  <Card icon="file">
    File extensions: `.yaml` or `.yml`
  </Card>
</CardGroup>

### Why YAML?

<AccordionGroup>
  <Accordion title="Clean, readable syntax" icon="sparkles">
    YAML's minimalist syntax makes it easy to read and write, reducing cognitive load compared to JSON or XML.
  </Accordion>

  <Accordion title="Supports comments" icon="comment">
    Unlike JSON, YAML allows you to document your configuration right where it matters.
  </Accordion>

  <Accordion title="Less verbose" icon="compress">
    No brackets, braces, or quotes clutter - just clean, indented structure.
  </Accordion>

  <Accordion title="Complex data structures" icon="diagram-project">
    Native support for nested objects, arrays, and advanced features like anchors and aliases.
  </Accordion>
</AccordionGroup>

---

## Basic Syntax

### Key-Value Pairs

Like the basic ingredients of chai: tea and water.

```yaml
# Simple key-value pairs
account_type: savings
status: active
holders: 2
processing_time: 5
```

### Comments

```yaml
# This is a single-line comment
account_type: savings  # Primary account type

# Multi-line notes
# Account must maintain
# minimum balance
```

### Indentation Rules

<Warning>
**CRITICAL:** YAML uses **spaces** for indentation, NOT tabs!
</Warning>

```yaml
# Good - 2 spaces (recommended)
bank_account:
  type: savings
  currency: INR

# Also valid - 4 spaces (But This is Bad Practice)
bank_account:
    type: savings
    currency: USD

# Bad - mixing spaces and tabs (will cause errors!)
# Don't do this!
```

---

## Data Types

### Strings

```yaml
# Unquoted strings
account_name: Kenil Gondaliya Savings

# Quoted strings (when special characters are present)
description: "Primary savings account for salary deposits"
tagline: 'Customer''s trusted financial partner'

# Multi-line strings - Literal style (preserves newlines)
baccount_notes: |
  Account opened in 2023
  Linked to salary deposits
  Has internet banking enabled

# Multi-line strings - Folded style (converts newlines to spaces)
account_summary: >
  This savings account is used for daily transactions.
  It includes ATM access and online banking.
```

### Numbers

```yaml
# Integers
account_balance: 25000
branch_code: 102

# Floats
interest_rate: 4.5
loan_amount: 150000.75

# Scientific notation
transaction_limit: 1.0e+4  # 10000

# Octal (prefix with 0o)
permission: 0o755

# Hexadecimal (prefix with 0x)
color_code: 0x1A73E8
```

### Booleans

```yaml
# Various ways to express true
is_active: true
kyc_verified: yes
internet_banking: on
has_credit_card: True

# Various ways to express false
is_frozen: false
loan_defaulted: no
overdraft_enabled: off
```

### Null Values

```yaml
# Different ways to represent null
middle_name: null
secondary_email: ~
nominee:
```

### Dates and Timestamps

```yaml
# ISO 8601 format
account_opened: 2025-01-15
last_transaction: 2025-01-15T10:30:00Z
last_login: 2025-01-15 08:30:00
```

---

## Collections

### Lists (Arrays)

```yaml
# Block style (recommended)
linked_cards:
  - debit_card
  - credit_card
  - prepaid_card

# Flow style (inline)
linked_cards: [debit_card, credit_card, prepaid_card] // (This is old format current not used)

# List of numbers
transaction_limits: [1000, 5000, 10000] // (This is old format current not used)

# Mixed types
account_flags:
  - "High Value Customer"
  - 5
  - true
```

### Nested Lists

```yaml
bank_services:
  - category: Accounts
    types:
      - Savings
      - Current
      - Fixed Deposit
  - category: Loans
    types:
      - Home Loan
      - Car Loan
      - Personal Loan
```

### Dictionaries (Objects/Maps)

```yaml
# Nested dictionaries
msavings_account:
  holder:
    name: John Doe
    id: CUST1023
  balance:
    available: 25000
    currency: USD
  settings:
    overdraft_limit: 5000
    daily_limit: 10000
  status:
    active: true
    kyc_verified: true
```

### List of Dictionaries

```yaml
accounts:
  - type: Savings
    balance: 25000
    currency: USD
    active: true
  - type: Current
    balance: 100000
    currency: USD
    active: true
  - type: Fixed Deposit
    balance: 50000
    currency: USD
    active: false
```

### Dictionary of Lists

```yaml
bank_inventory:
  account_types:
    - Savings
    - Current
    - Fixed Deposit
  loan_types:
    - Home Loan
    - Car Loan
    - Education Loan
  cards:
    - Debit Card
    - Credit Card
    - Virtual Card
```

---

## Advanced Features

### Anchors and Aliases (DRY - Don't Repeat Yourself)

<Tip>
Like making a chai concentrate and using it multiple times!
</Tip>

```yaml
# Define an anchor with &
default_account_settings: &default_settings (&default_settings Called Anchor)
  currency: USD
  daily_limit: 10000
  overdraft_enabled: false

# Reference it with *
john_account:
  <<: *default_settings
  account_type: savings
  balance: 25000

business_account:
  <<: *default_settings
  account_type: current
  overdraft_enabled: true
  balance: 100000

```

### Merge Keys

```yaml
# Define reusable components
base_loan: &base_loan
  interest_rate: 7.5
  tenure_years: 5

premium_loan: &premium_loan
  <<: *base_loan
  priority_processing: true

home_loan:
  <<: *base_loan
  amount: 200000

vip_home_loan:
  <<: *premium_loan
  amount: 500000
```

### Multi-line Keys

```yaml
? |
  This is a very long key
  that spans multiple lines
: "And this is its value"
```

### Complex Mapping Keys

```yaml
# Using lists or objects as keys
? - savings_account
  - current_account
  - fixed_deposit
: "Retail banking products"

? {customer_id: 1023, account_type: savings}
: "Primary customer savings account"

? {loan_type: home_loan, tenure_years: 20}
: "Long-term secured loan product"

? - debit_card
  - credit_card
  - virtual_card
: "Card services offered by the bank"
```

### Explicit Data Types

```yaml
# Force string interpretation
account_number: !!str 00123456789
version: !!str 1.0

# Force integer
transaction_count: !!int "150"

# Force float
interest_rate: !!float "4.5"

# Set
authorized_roles: !!set
  ? manager
  ? teller
  ? auditor
```

### YAML Tags

```yaml
# Custom types
special_date: !date 2025-01-15
custom_object: !MyClass
  property: value
```

---

## Common Pitfalls

### 1. Tabs vs Spaces

<Warning>
Using tabs instead of spaces will break your YAML!
</Warning>

```yaml
# ❌ WRONG - using tabs
account:
	type: saving	# This will break!

# ✅ CORRECT - using spaces
account:
  type: current
```

### 2. Inconsistent Indentation

```yaml
# ❌ WRONG
bank_account:
  services:
    - savings
    - current   # Extra space!
  - fixed_deposit   # Wrong indentation level!

# ✅ CORRECT
bank_account:
  services:
    - savings
    - current
    - fixed_deposit
```

### 3. Special Characters in Unquoted Strings

```yaml
# ❌ WRONG
description: Savings & Current: Premium Plan!  # & and : are special

# ✅ CORRECT
description: "Savings & Current: Premium Plan!"
```

### 4. Boolean Confusion

<Warning>
Watch out for the Norway problem! `no` is interpreted as `false`.
</Warning>

```yaml
# These are ALL interpreted as booleans, not strings!
kyc_completed: yes
loan_approved: no
internet_banking: on
account_locked: off

# If you want strings, quote them:
country_code: "no"   # Norway
customer_response: "yes"
```

### 5. Number Interpretation

```yaml
# ❌ These might not be what you expect
account_number: 00123456789   # Leading zeros removed
interest_rate: 4.50           # May become 4.5
branch_code: 0123             # Interpreted as octal

# ✅ CORRECT - quote them
account_number: "00123456789"
interest_rate: "4.50"
branch_code: "0123"
```

### 6. Empty Values

```yaml
# These are different!
nominee:          # null/empty
middle_name: ""   # empty string
secondary_email: null
alternate_contact: ~
```

---

## Real-World Examples

### 1. Chai Shop Configuration

```yaml
# config.yaml
bank:
  name: Secure Trust Bank
  headquarters:
    address: "100 Finance Street"
    city: New York
    country: USA
    coordinates:
      lat: 40.7128
      lng: -74.0060
  operating_hours:
    weekdays:
      open: "09:00"
      close: "17:00"
    weekend:
      open: "10:00"
      close: "14:00"
  services:
    - id: 1
      name: Savings Account
      interest_rate: 4.5
      active: true
    - id: 2
      name: Home Loan
      interest_rate: 7.5
      active: true
  staff:
    - name: Alice Johnson
      role: Branch Manager
      experience_years: 12
    - name: Mark Smith
      role: Loan Officer
      experience_years: 5
```

### 2. CI/CD Pipeline (Chai Delivery App)

```yaml
# .github/workflows/chai-app.yml
name: Digital Banking Platform CI/CD

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

env:
  NODE_VERSION: '18'
  APP_NAME: digital-banking-platform
  REGISTRY: bank-registry.io

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ env.NODE_VERSION }}

      - name: Install dependencies
        run: npm ci

      - name: Run tests
        run: npm test

      - name: Generate coverage
        run: npm run coverage

  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Build Docker image
        run: |
          docker build -t ${{ env.APP_NAME }}:${{ github.sha }} .

      - name: Push to registry
        run: |
          docker push ${{ env.APP_NAME }}:${{ github.sha }}

  deploy:
    needs: build
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
      - name: Deploy to Kubernetes cluster
        run: |
          kubectl set image deployment/${{ env.APP_NAME }} \
            banking-app=${{ env.REGISTRY }}/${{ env.APP_NAME }}:${{ github.sha }}

      - name: Verify deployment rollout
        run: |
          kubectl rollout status deployment/${{ env.APP_NAME }}
```

### 3. Docker Compose (Chai Shop Microservices)

```yaml
# docker-compose.yml
version: '3.8'

services:
  # Frontend service
  banking-frontend:
    image: bank-platform/frontend:latest
    build:
      context: ./frontend
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
    environment:
      - REACT_APP_API_URL=http://localhost:8080
      - NODE_ENV=production
    depends_on:
      - banking-backend
    networks:
      - banking-network

  # Backend API service
  banking-backend:
    image: bank-platform/backend:latest
    build:
      context: ./backend
      dockerfile: Dockerfile
    ports:
      - "8080:8080"
    environment:
      - DATABASE_URL=postgresql://bank_user:bank_pass@postgres:5432/bank_db
      - REDIS_URL=redis://redis:6379
      - JWT_SECRET=${JWT_SECRET}
    depends_on:
      - postgres
      - redis
    volumes:
      - ./logs:/app/logs
    networks:
      - banking-network

  # Database
  postgres:
    image: postgres:15-alpine
    environment:
      - POSTGRES_USER=bank_user
      - POSTGRES_PASSWORD=bank_pass
      - POSTGRES_DB=bank_db
    volumes:
      - postgres_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"
    networks:
      - banking-network

  # Cache
  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data
    networks:
      - banking-network

volumes:
  postgres_data:
  redis_data:

networks:
  banking-network:
    driver: bridge
```

### 4. Kubernetes Deployment

```yaml
# k8s/banking-app-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: digital-banking-app
  namespace: production
  labels:
    app: digital-banking
    version: v1
spec:
  replicas: 3
  selector:
    matchLabels:
      app: digital-banking
  template:
    metadata:
      labels:
        app: digital-banking
        version: v1
    spec:
      containers:
        - name: banking-app
          image: bank-platform/app:1.0.0
          ports:
            - containerPort: 8080
              name: http
          env:
            - name: DATABASE_URL
              valueFrom:
                secretKeyRef:
                  name: banking-secrets
                  key: database-url
            - name: REDIS_HOST
              value: "redis-service"
            - name: LOG_LEVEL
              value: "info"
          resources:
            requests:
              memory: "256Mi"
              cpu: "250m"
            limits:
              memory: "512Mi"
              cpu: "500m"
          livenessProbe:
            httpGet:
              path: /health
              port: 8080
            initialDelaySeconds: 30
            periodSeconds: 10
          readinessProbe:
            httpGet:
              path: /ready
              port: 8080
            initialDelaySeconds: 5
            periodSeconds: 5
---
apiVersion: v1
kind: Service
metadata:
  name: digital-banking-service
  namespace: production
spec:
  selector:
    app: digital-banking
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: LoadBalancer
```

### 5. Application Configuration

```yaml
# application.yaml
application:
  name: Digital Banking Platform
  version: 1.0.0

server:
  port: 8080
  host: 0.0.0.0
  timeout:
    read: 30s
    write: 30s
    idle: 120s

database:
  primary:
    host: localhost
    port: 5432
    name: bank_db
    username: bank_user
    password: ${DB_PASSWORD}  # From environment variable
    pool:
      min: 5
      max: 20
      idle_timeout: 300
  replica:
    host: replica.localhost
    port: 5432
    name: bank_db
    username: bank_reader
    password: ${DB_REPLICA_PASSWORD}

cache:
  redis:
    host: localhost
    port: 6379
    db: 0
    ttl: 3600
    prefix: "bank:"

logging:
  level: info
  format: json
  outputs:
    - type: file
      path: /var/log/banking-app.log
      max_size: 100MB
      max_backups: 5
    - type: stdout

features:
  payment_processing:
    enabled: true
    provider: stripe
    test_mode: false
  notifications:
    enabled: true
    channels:
      email: true
      sms: true
      push: true
  fraud_detection:
    enabled: true
    real_time_monitoring: true
    risk_threshold: 0.8

bank_products:
  categories:
    - name: Accounts
      items:
        - name: Savings Account
          interest_rate: 4.5
          minimum_balance: 1000
        - name: Current Account
          interest_rate: 0
          minimum_balance: 5000
    - name: Loans
      items:
        - name: Home Loan
          interest_rate: 7.5
          max_tenure_years: 30
        - name: Personal Loan
          interest_rate: 12.0
          max_tenure_years: 5
```

---

## Best Practices

### 1. Use Consistent Indentation

```yaml
# Choose 2 or 4 spaces and stick with it
# 2 spaces (recommended)
bank_account:
  type: savings
  currency: USD
  features:
    - internet_banking
    - debit_card
```

### 2. Quote Strings When Necessary

```yaml
# Quote strings with special characters
description: "Savings & Current: Premium Banking Plan!"
website: "https://digitalbank.com"
account_number: "00123456789"
```

### 3. Use Meaningful Key Names

```yaml
# ❌ Not clear
a: savings
b: 4.5

# ✅ Clear and descriptive
account_type: savings
interest_rate_percentage: 4.5
```

### 4. Keep It Simple

```yaml
# Avoid over-nesting when possible
# Instead of deep nesting, use flat structures with namespaced keys
loan_home_interest_rate: 7.5
loan_home_max_tenure_years: 30
```

### 5. Use Comments Wisely

```yaml
# Document complex or non-obvious configurations
server:
  # Increased timeout for high transaction volume
  timeout: 60
  # Connection pool sized for peak hours (1000 concurrent users)
  pool_size: 200
```

### 6. Leverage Anchors for Reusability

```yaml
# Define common patterns once
default_account_settings: &defaults
  currency: USD
  daily_limit: 10000
  overdraft_enabled: false

savings_account:
  <<: *defaults
  interest_rate: 4.5

current_account:
  <<: *defaults
  overdraft_enabled: true
```

### 7. Validate Your YAML

<CardGroup cols={3}>
  <Card title="YAML Lint" icon="globe" href="http://www.yamllint.com"> Online validator </Card>

  <Card title="yamllint CLI" icon="terminal" href="https://github.com/adrienverge/yamllint"> 
  Command-line linter </Card>

  <Card title="yq" icon="filter" href="https://github.com/mikefarah/yq"> YAML processor </Card>
</CardGroup>

### 8. Use Version Control Friendly Format

```yaml
# Prefer block style for better diffs
bank_services:
  - savings_account
  - current_account
  - home_loan

# Instead of flow style
# bank_services: [savings_account, current_account, home_loan]
```

---

## Quick Reference Card

```yaml
# 🏦 YAML Syntax Cheat Sheet (Banking Example)

# Key-Value
key: value

# Strings
string: "quoted string"
multiline: |
  Line 1
  Line 2

# Numbers
integer: 42
float: 3.14

# Booleans
boolean: true

# Null
empty: null

# Lists
list:
  - item1
  - item2

# Dictionary
dict:
  key1: value1
  key2: value2

# Anchor & Alias
base: &anchor
  shared: data
use:
  <<: *anchor

# Comments
# This is a comment
```

---

## Practice Exercises

<AccordionGroup>
  <Accordion title="Exercise 1: Create a Bank Account Configuration" icon="building-columns">
    Create a YAML file for a customer bank account with:
    - Name and description
    - Metadata (branch, opening date, status)
  </Accordion>

  <Accordion title="Exercise 2: Banking Application Configuration" icon="gear">
    Design a YAML configuration for a digital banking app with:
    - Database settings
    - API endpoints
    - Feature flags
    - Feature flags (KYC, fraud detection, payments)
  </Accordion>

  <Accordion title="Exercise 3: Docker Compose for Banking Platform" icon="docker">
    Create a `docker-compose.yml` for a banking application with:
    - Web frontend
    - API backend
    - Database
    - Cache layer
  </Accordion>
</AccordionGroup>

---

## Tools and Resources

### Validators

<CardGroup cols={2}>
  <Card title="YAML Lint" icon="check" href="http://www.yamllint.com">
    Online validator for quick testing
  </Card>
  <Card title="yamllint" icon="terminal" href="https://github.com/adrienverge/yamllint">
    CLI linter for automation
  </Card>
</CardGroup>

### Parsers

- **Python**: PyYAML, ruamel.yaml
- **JavaScript**: js-yaml
- **Go**: [gopkg.in/yaml.v3](http://gopkg.in/yaml.v3)
- **Ruby**: psych (built-in)
- **Java**: SnakeYAML

### Editors with YAML Support

- VS Code (with YAML extension)
- IntelliJ IDEA
- Sublime Text
- Vim/Neovim (with yaml plugins)

---


*Happy YAML-ing! 🏦*