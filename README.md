# playwright-js-e2e-course
🎭 Complete 1-Month Step-by-Step Course to Master Playwright with JavaScript – From Beginner to Advanced. Includes Setup, Core Concepts, Projects, CI/CD &amp; Reporting!

# 🎭 Playwright JS E2E Course

Welcome to the **Playwright with JavaScript - 1 Month Bootcamp**!  
This repo includes all the source code, projects, notes, and examples covered in the course.

---

## 📚 What You'll Learn
- Playwright Setup & Basics
- Writing and Running Tests
- Locators, Assertions, Hooks
- Device Emulation, Auth, APIs
- Page Object Model (POM)
- Network Mocking & Debugging
- CI/CD with GitHub Actions
- Reporting with HTML & Allure

---

## 📦 Tech Stack
- [Playwright](https://playwright.dev/)
- JavaScript (ES6+)
- Node.js / npm
- VS Code
- GitHub Actions
- Allure Reports

---
Playwright Automation Learning Roadmap with JavaScript (1 Month)
From Beginner to Intermediate Level

🎯 Prerequisites
JavaScript ES6+ (async/await, promises)

Basic HTML/CSS selector knowledge

Node.js (v16+) installed

VS Code or similar IDE

📅 Week 1: Playwright Foundations & Setup
Day 1-2: Introduction & Installation
Install: Node.js, Playwright, VS Code

Setup project:

bash
mkdir playwright-tests
cd playwright-tests
npm init -y
npm init playwright@latest
Explore: Playwright Test runner, folder structure

Run first test: npx playwright test

Resource:
🔗 Playwright Installation & First Test - TechTalk

 Day 3-4: Basic Test Writing
Learn:

test.describe(), test()

Page navigation: page.goto()

Locators: page.locator(), page.getByRole()

Basic assertions: expect()

Practice: Write 5 basic tests

Resource:
🔗 Playwright Beginner Tutorial - LetCode

Day 5-7: Locators & Assertions Deep Dive
Learn:

Best Practice Locators: getByRole(), getByText(), getByLabel()

CSS/XPath selectors

Assertions: toHaveText(), toBeVisible(), toHaveCount()

Auto-waiting concept

Project: Test demo sites (demoqa.com, saucedemo.com)

Resource:
🔗 Playwright Locators Masterclass - automateNow

📅 Week 2: Core Interactions & Features
Day 8-9: User Interactions
Learn:

Click actions: .click(), .dblclick()

Fill forms: .fill(), .type()

Keyboard: .press(), .keyboard.type()

Mouse: .hover(), .dragAndDrop()

Practice: Complete form automation

Resource:
🔗 Playwright Interactions - Testing Mini Bytes

Day 10-12: Advanced Features
Learn:

Fixtures: test.use()

Test Hooks: beforeEach(), afterEach()

Screenshots & Videos: Automatic capture

Trace Viewer: Debugging tool

Practice: Configure project with screenshots on failure

Resource:
🔗 Playwright Configuration - TechTalk

Day 13-14: API Testing & Mocking
Learn:

page.route() for network mocking

API request context: request.get(), request.post()

Mock responses and intercept requests

Project: Mock API responses for faster tests

Resource:
🔗 Playwright API Testing - Testing Mini Bytes

📅 Week 3: Advanced Patterns & Framework
Day 15-17: Page Object Model (POM)
Learn:

Create Page Object classes

Base page structure

Component-based design

Best practices for maintainability

Project: Refactor Week 2 tests using POM

Resource:
🔗 Page Object Model in Playwright - automateNow

Day 18-20: Advanced Scenarios
Learn:

Multiple tabs/windows: page.context()

Iframes: frameLocator()

File upload/download: setInputFiles()

Authentication: Storage state

Visual testing: toHaveScreenshot()

Practice: Handle complex UI scenarios

Resource:
🔗 Advanced Playwright Scenarios - LetCode

Day 21: Parallel Execution & Configuration
Learn:

Parallel test execution

playwright.config.js deep dive

Multiple projects (chromium, firefox, webkit)

Sharding for CI

Resource:
🔗 Playwright Parallel Execution - TechTalk

📅 Week 4: Real Projects & CI/CD
Day 22-24: E-commerce Test Suite
Build complete test suite for:

User registration/login

Product search and filtering

Shopping cart operations

Checkout process

Implement: POM, fixtures, custom assertions

Test Site: saucedemo.com or nopCommerce demo

Day 25-27: CI/CD Integration
Learn:

GitHub Actions for Playwright

Dockerized Playwright tests

Test reports: HTML, Allure, JUnit

Slack/email notifications

Setup:

yaml
# .github/workflows/playwright.yml
name: Playwright Tests
on: [push]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
      - run: npm ci
      - run: npx playwright install --with-deps
      - run: npx playwright test
      - uses: actions/upload-artifact@v3
        if: always()
        with:
          name: playwright-report
          path: playwright-report/
Resource:
🔗 Playwright CI/CD - Microsoft Developer

Day 28-30: Portfolio Project & Optimization
Create portfolio framework with:

Custom reporters

Global setup/teardown

Environment configuration

Performance testing

Optimize: Test execution speed

Learn: Custom fixtures, test annotations

🆓 Free Learning Resources
YouTube Channels:
Microsoft Developer - Official Playwright tutorials

LetCode - Practical projects & tutorials

Testing Mini Bytes - Short, focused lessons

automateNow - Framework building

TechTalk - Advanced concepts

Free Courses & Documentation:
Official Playwright Docs (playwright.dev) - Excellent & comprehensive

Playwright Test Runner (github.com/microsoft/playwright-test)

Playwright Examples (github.com/microsoft/playwright-examples)

freeCodeCamp Playwright Tutorial (check their YouTube)

Practice Websites:
DemoQA (demoqa.com) - Forms, widgets, elements

SauceDemo (saucedemo.com) - E-commerce practice

The Internet (the-internet.herokuapp.com) - Various scenarios

OrangeHRM Demo (orangehrm-demo-7x.orangehrmlive.com) - Enterprise app

📁 Project Structure
text
playwright-framework/
├── tests/
│   ├── pages/              # Page Objects
│   │   ├── BasePage.js
│   │   ├── LoginPage.js
│   │   └── CartPage.js
│   ├── fixtures/           # Test fixtures
│   │   └── test-data.json
│   ├── specs/              # Test files
│   │   ├── login.spec.js
│   │   └── checkout.spec.js
│   └── utils/              # Utilities
│       └── helpers.js
├── playwright.config.js    # Configuration
├── package.json
├── .github/workflows/      # CI/CD
└── README.md
🔧 Sample Test with POM
javascript
// tests/pages/LoginPage.js
class LoginPage {
  constructor(page) {
    this.page = page;
    this.username = page.getByPlaceholder('Username');
    this.password = page.getByPlaceholder('Password');
    this.loginBtn = page.getByRole('button', { name: 'Login' });
  }
  
  async navigate() {
    await this.page.goto('/');
  }
  
  async login(user, pass) {
    await this.username.fill(user);
    await this.password.fill(pass);
    await this.loginBtn.click();
  }
}

// tests/specs/login.spec.js
const { test, expect } = require('@playwright/test');
const { LoginPage } = require('../pages/LoginPage');

test.describe('Login Tests', () => {
  test('Successful login', async ({ page }) => {
    const loginPage = new LoginPage(page);
    await loginPage.navigate();
    await loginPage.login('standard_user', 'secret_sauce');
    
    await expect(page).toHaveURL(/inventory/);
    await expect(page.getByText('Products')).toBeVisible();
  });
});
🚀 Daily Practice Plan
Morning (30 min): Watch tutorials/concepts
Afternoon (1 hour): Implement new features
Evening (30 min): Refactor, debug, document
Weekly: Complete one mini-project

💼 Job-Ready Skills After 1 Month
✅ Write maintainable Playwright tests
✅ Implement Page Object Model
✅ Test APIs and mock responses
✅ Run tests in parallel
✅ Integrate with CI/CD
✅ Generate test reports
✅ Handle complex UI scenarios
✅ Debug with Trace Viewer

🎯 Interview Topics
Playwright vs Cypress vs Selenium

Auto-waiting mechanism

Parallel execution strategies

Cross-browser testing

Network interception use cases

Performance advantages

🌟 Pro Tips
Use getByRole() for accessible, stable locators

Leverage Trace Viewer for debugging

Store auth state to speed up tests

Use fixtures for test isolation

Implement custom reporters for better insights

Test on mobile viewports

📈 Learning Path After Month 1
TypeScript with Playwright

Visual regression testing

Accessibility testing (Axe-core)

Performance monitoring

Custom test runners

Plugin development

🔗 Community & Support
Playwright Discord (active community)

GitHub Discussions (official repo)

Stack Overflow (#playwright tag)

Reddit r/QualityAssurance

🏆 Final Project Ideas
Complete E-commerce Test Suite with 50+ tests

API + UI Integration Framework

Custom HTML Reporter with dashboards

Dockerized Test Runner for team use

Performance Benchmark Suite

Remember: Playwright's strength is in its modern architecture and excellent tooling. Focus on understanding the core concepts rather than memorizing syntax.

Share your progress with #PlaywrightTesting #TestAutomation on LinkedIn/Twitter!

Need help? Join Playwright's Discord server – very welcoming community!


