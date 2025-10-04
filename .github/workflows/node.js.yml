name: Node.js CI/CD Pipeline

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  compile:
    runs-on: Agent-1
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '22'   # use stable LTS unless you really need 23
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Build project
        run: npm run build --if-present

      - name: Run tests
        run: npm test

      - name: Frontend Compilation (Syntax Check)
        run: |
          cd client
          find . -name "*.js" -exec node --check {} \;

      - name: Backend Compilation (Syntax Check)
        run: |
          cd api
          find . -name "*.js" -exec node --check {} \;

  gitleaks-scan:
    runs-on: Agent-1
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Run Gitleaks
        uses: zricethezav/gitleaks-action@v2
