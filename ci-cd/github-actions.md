# GitHub Actions — CI for QA

PURPOSE: Run tests on push or pull request to ensure code quality.

## Maven + Selenium Workflow
```yaml
name: Selenium Tests
on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Setup Java
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Cache Maven packages
        uses: actions/cache@v4
        with:
          path: ~/.m2/repository
          key: ${{ runner.os }}-maven-${{ hashFiles('**/pom.xml') }}
          restore-keys: |
            ${{ runner.os }}-maven-

      - name: Install dependencies
        run: mvn clean install -DskipTests

      - name: Run tests
        run: mvn test
```

## Tips
- Upload test artifacts or screenshots as workflow artifacts on failure
- Use matrix builds to run across Java versions or browsers
