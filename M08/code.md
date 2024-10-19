
# CI/CD Pipeline Schulung

## Themen

1. Erstellen einer einfachen CI/CD-Pipeline
2. Konfiguration von GitHub Actions oder GitLab CI
3. Tests und Linting in der Pipeline ausführen

## 1. Erstellen einer einfachen CI/CD-Pipeline

### Live Coding Beispiel

In `.github/workflows/ci.yml` (GitHub Actions):

```yaml
name: CI Pipeline

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Install dependencies
      run: npm install

    - name: Build application
      run: npm run build
```

In `.gitlab-ci.yml` (GitLab CI):

```yaml
stages:
  - build

build-job:
  stage: build
  script:
    - npm install
    - npm run build
```

## 2. Konfiguration von GitHub Actions oder GitLab CI

### Live Coding Beispiel für GitHub Actions

In `.github/workflows/ci.yml`:

```yaml
name: Node.js CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '14'

    - name: Install dependencies
      run: npm install

    - name: Run Tests
      run: npm test
```

### Live Coding Beispiel für GitLab CI

In `.gitlab-ci.yml`:

```yaml
image: node:14

stages:
  - test
  - build

test-job:
  stage: test
  script:
    - npm install
    - npm test
```

## 3. Tests und Linting in der Pipeline ausführen

### Live Coding Beispiel

In `.github/workflows/ci.yml` für Tests und Linting:

```yaml
name: Lint and Test

on: [push, pull_request]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Install dependencies
      run: npm install

    - name: Lint code
      run: npm run lint

  test:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Install dependencies
      run: npm install

    - name: Run Tests
      run: npm test
```

### Beispiel für GitLab CI

In `.gitlab-ci.yml`:

```yaml
stages:
  - lint
  - test

lint-job:
  stage: lint
  script:
    - npm install
    - npm run lint

test-job:
  stage: test
  script:
    - npm install
    - npm test
```