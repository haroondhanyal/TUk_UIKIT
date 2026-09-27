# TUk_UIKIT - Cypress UI Automation

## Overview

TUk_UIKIT is a **Cypress-based UI automation project** designed for end-to-end testing of web application functionality.

The project uses **JavaScript, Cypress, and Cypress XPath** to automate browser interactions, validate UI behavior, and provide a simple foundation for building scalable regression automation suites.

The repository currently contains the standard Cypress automation structure along with Cypress configuration and Node.js dependency management.

---

## Technology Stack

- **JavaScript**
- **Node.js**
- **Cypress**
- **Cypress XPath**
- **npm**
- **End-to-End UI Automation**

---

## Automation Purpose

The main purpose of this project is to automate web application workflows and verify that the UI behaves as expected.

The automation framework can be used for:

- Functional testing
- UI validation
- Regression testing
- Smoke testing
- End-to-end testing
- Form validation
- Navigation testing
- User workflow validation
- Positive and negative scenarios

---

## Current Project Structure

```text
TUk_UIKIT/
│
├── cypress/
│   └── Cypress automation files
│
├── cypress.config.js
│   └── Cypress project configuration
│
├── package.json
│   └── Project dependencies and npm configuration
│
├── package-lock.json
│   └── Locked dependency versions
│
└── README.md
    └── Project documentation
```

The project is configured using Cypress's modern `e2e` configuration structure.

---

## Dependencies

The project currently uses:

```json
"cypress": "^12.17.2",
"cypress-xpath": "^2.0.1"
```

Cypress is responsible for browser automation, while `cypress-xpath` allows XPath selectors to be used when locating elements.

---

## Automation Architecture

A Cypress automation flow typically works as follows:

```text
Test Scenario
     ↓
Test Specification
     ↓
Cypress Commands
     ↓
Element Locators
     ↓
Browser Interaction
     ↓
Assertions
     ↓
Pass / Fail Result
```

---

## Cypress Test Flow

A typical automated test can perform the following actions:

```text
Launch Application
        ↓
Navigate to Required Page
        ↓
Locate UI Element
        ↓
Perform User Action
        ↓
Validate Application Response
        ↓
Apply Assertions
        ↓
Test Pass / Fail
```

Examples of user actions include:

- Clicking buttons
- Entering text
- Selecting values
- Navigating between pages
- Submitting forms
- Validating messages
- Verifying displayed information

---

## Cypress Folder

The `cypress/` directory contains the actual automation implementation.

A scalable Cypress structure can be organized as:

```text
cypress/
│
├── e2e/
│   ├── login.cy.js
│   ├── dashboard.cy.js
│   └── user-flow.cy.js
│
├── fixtures/
│   └── testdata.json
│
├── support/
│   ├── commands.js
│   └── e2e.js
│
└── pages/
    ├── LoginPage.js
    └── DashboardPage.js
```

---

## Test Specifications

The `e2e` directory should contain test scenarios.

Example:

```javascript
describe('Application Login', () => {

  it('should login successfully with valid credentials', () => {

    cy.visit('https://example.com')

    cy.get('#username').type('testuser')
    cy.get('#password').type('password')

    cy.get('#login').click()

    cy.url().should('include', '/dashboard')

  })

})
```

The test follows the standard Cypress structure:

```text
describe()
   ↓
it()
   ↓
Actions
   ↓
Assertions
```

---

## XPath Support

The project includes `cypress-xpath`.

This allows XPath-based element identification.

Example:

```javascript
cy.xpath("//button[text()='Login']").click()
```

XPath can be useful where reliable CSS selectors or IDs are not available.

However, wherever possible, stable attributes such as:

```text
data-testid
id
name
```

should be preferred for more maintainable automation.

---

## Cypress Configuration

The project uses:

```text
cypress.config.js
```

The current configuration enables Cypress **E2E testing** and provides the `setupNodeEvents()` method for future Node.js event customization.

The configuration can later be expanded with:

```javascript
const { defineConfig } = require("cypress");

module.exports = defineConfig({

  e2e: {

    baseUrl: "https://example.com",

    viewportWidth: 1280,
    viewportHeight: 720,

    defaultCommandTimeout: 10000,

    setupNodeEvents(on, config) {
      // Node events
    },

  },

});
```

---

## Page Object Model

For larger automation projects, a **Page Object Model (POM)** structure can be introduced.

Example:

```text
cypress/
└── pages/
    ├── LoginPage.js
    ├── HomePage.js
    └── UserPage.js
```

Example page:

```javascript
class LoginPage {

  username = '#username'
  password = '#password'
  loginButton = '#login'

  login(username, password) {

    cy.get(this.username).type(username)
    cy.get(this.password).type(password)
    cy.get(this.loginButton).click()

  }

}

export default new LoginPage()
```

Test:

```javascript
import LoginPage from '../pages/LoginPage'

describe('Login Tests', () => {

  it('valid login', () => {

    cy.visit('/login')

    LoginPage.login(
      'testuser',
      'password'
    )

  })

})
```

This improves:

- Code reuse
- Maintainability
- Readability
- Scalability
- Locator management

---

## Test Data Management

Test data should preferably be kept separately from test scripts.

Example:

```text
cypress/
└── fixtures/
    └── users.json
```

Example:

```json
{
  "username": "testuser",
  "password": "password123"
}
```

Usage:

```javascript
cy.fixture('users').then((user) => {

  cy.get('#username').type(user.username)

})
```

This supports data-driven automation.

---

## Assertions

Cypress provides built-in assertions using Chai.

Examples:

```javascript
cy.get('.success-message')
  .should('be.visible')
```

```javascript
cy.get('.username')
  .should('contain', 'Haroon')
```

```javascript
cy.url()
  .should('include', '/dashboard')
```

Assertions determine whether the automated scenario passes or fails.

---

## Installation

Clone the repository:

```bash
git clone https://github.com/haroondhanyal/TUk_UIKIT.git
```

Move into the project:

```bash
cd TUk_UIKIT
```

Install dependencies:

```bash
npm install
```

---

## Run Cypress

Open Cypress Test Runner:

```bash
npx cypress open
```

This launches the interactive Cypress interface where tests can be selected and executed.

---

## Headless Execution

Run all tests without opening the Cypress UI:

```bash
npx cypress run
```

This mode is suitable for:

- CI/CD pipelines
- Automated regression runs
- Scheduled execution

---

## Run Specific Browser

Chrome:

```bash
npx cypress run --browser chrome
```

Electron:

```bash
npx cypress run --browser electron
```

---

## Recommended Framework Structure

For a more professional automation framework, the repository can eventually follow:

```text
TUk_UIKIT/
│
├── cypress/
│   │
│   ├── e2e/
│   │   ├── smoke/
│   │   ├── regression/
│   │   └── functional/
│   │
│   ├── pages/
│   │   ├── LoginPage.js
│   │   └── DashboardPage.js
│   │
│   ├── fixtures/
│   │   └── testdata.json
│   │
│   └── support/
│       ├── commands.js
│       └── e2e.js
│
├── reports/
├── screenshots/
├── videos/
├── cypress.config.js
├── package.json
├── package-lock.json
├── .gitignore
└── README.md
```

---

## Recommended Automation Workflow

```text
Requirement / User Story
          ↓
Identify Test Scenarios
          ↓
Prepare Test Data
          ↓
Create Page Objects
          ↓
Develop Cypress Tests
          ↓
Execute Locally
          ↓
Validate Assertions
          ↓
Generate Evidence
          ↓
Run Regression
          ↓
CI/CD Execution
```

---

## Framework Benefits

### Fast Execution

Cypress automatically waits for elements and application states, reducing the need for manual synchronization.

### Easy Debugging

Interactive execution provides:

- Command logs
- Browser snapshots
- Error details
- Screenshots
- Video support

### Reliable Assertions

Cypress continuously retries commands and assertions until the configured timeout is reached.

### Maintainability

Separating test cases, page objects, test data, and reusable commands makes the project easier to maintain.

### Scalability

New modules and test scenarios can be added without changing the complete automation architecture.

---

## Future Improvements

The project can be enhanced by adding:

- Page Object Model
- Custom Cypress commands
- Fixtures for test data
- Environment configuration
- API testing with `cy.request()`
- Mochawesome reporting
- Screenshots on failure
- Video recording
- Smoke and regression suites
- Test tagging
- GitHub Actions CI/CD
- Cross-browser execution
- Parallel execution

---

## CI/CD Integration

The framework can later be integrated with GitHub Actions.

Example workflow:

```text
Code Push
    ↓
GitHub Actions
    ↓
npm install
    ↓
Cypress Test Execution
    ↓
Generate Results
    ↓
Pass / Fail Build
```

This allows automation tests to execute automatically on:

- Push
- Pull request
- Release
- Scheduled regression execution

---

## Project Summary

TUk_UIKIT is a lightweight **Cypress end-to-end UI automation project** built with JavaScript.

The framework demonstrates:

- Cypress setup
- JavaScript UI automation
- Browser-based testing
- End-to-end automation
- XPath locator support
- UI interaction
- Assertions
- Functional testing
- Regression testing foundation

The project can be extended into a complete Cypress automation framework by introducing Page Object Model, fixtures, reusable commands, reporting, and CI/CD integration.
