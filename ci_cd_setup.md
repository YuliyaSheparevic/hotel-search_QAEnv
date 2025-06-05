The CI/CD automation ensures that the test suite runs automatically during development and production builds. This process helps developers:

Validate code changes through automated unit tests, widget tests, and integration tests.
Avoid regressions by running a consistent and repeatable suite.
Generate reports and logs automatically for debugging and quality assurance.

It is reasonable to choose GitHab Actions because it is integrated natively with GitHub repositories and allows creating custom workflows to automate testing and deployment.

1. **Test Suite Integration**
- **Unit and Widget Tests** focus on verifying small, isolated components of the application. These tests are executed using command : flutter test
- **Integration Tests** involve running real workflows, simulating user actions, and validating the behavior of multiple components. These tests are executed using command: flutter drive --target=integration_test/<test_file.dart>

2. **Build Workflow for CI/CD**

Create YAML file for GitHub Actions (.github/workflows/ci.yml) where all information about running automation process should exist:
1. Name of the pipeline
  
   name: Flutter App CI

2. When CI/CD pipeline will trigger (e.g. after every MR, after pulling MR into Main or based on scedule: once a day, once a hour and so on)

 on:
  push:
    branches:
      - main
      
3. Jobs and Steps in this Job (Install some dependencies, Install Flutter and so on) and then Run unit and widget tests and Run integration tests

    // Unit and Widget Tests
    - name: Run unit and widget tests
      run: flutter test

    // Integration Tests
    - name: Run integration tests
      run: |
        flutter drive --target=integration_test/app_test.dart
4. Add some artifacts if needed (save logs, add possibility to do a screenshots in case of falures, generated reports and so on)
     // Save Logs
    - name: Save Test Results
      uses: actions/upload-artifact@v3
      with:
        name: flutter-test-logs
        path: build/test-results

5. Adding Notifications via Slack or MTeams

 For example, in GitHub Actions, you can trigger Slack notifications using:

 steps:
  - name: Send notification to Slack
    uses: slackapi/slack-github-action@v1.16.0
    with:
      notify_failure: true
