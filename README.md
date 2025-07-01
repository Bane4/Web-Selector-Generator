Selector Generator
A browser-based tool that generates robust CSS and XPath selectors for automated UI testing. Built to support multiple testing frameworks and languages with a flexible set of options.

🔧 Features
Paste any target HTML element to generate selectors.

(Optional) Provide full DOM context to build full-path selectors.

Supports multiple testing frameworks:

Playwright

Selenium

Cypress

Puppeteer

WebdriverIO

Supports multiple programming languages:

JavaScript

Python

Java

C#

Generates and displays three types of selectors:

Best Selector: Chooses the most reliable option (e.g., id, data-test-id, or minimal unique path).

CSS Selector

XPath Selector

Copy each selector to clipboard with a single click.

Option to avoid dynamic class names (e.g., those starting with sc-, tw-, or long hashes).

Option to prefer text content in selectors for better readability.

Option to prefer deepest matching element when there are multiple matches.

Option to build selector from root of the document or just relative to the matched element.

Fully client-side — no dependencies, no uploads, no frameworks.

🚀 How to Use
Paste the HTML of the element you want to target in the Target Element box.

(Optional) Paste the full HTML of the page in the Full DOM box.

Choose your framework and language from the dropdowns.

Adjust preferences:

Avoid dynamic classes

Use text content in selector

Prefer most deeply nested match

Build selector from document root

Click Generate Selector.

Copy the Best, CSS, or XPath selector using the buttons below the results.

💡 Example Use Case
You're writing a Playwright test in JavaScript. You paste in a button’s HTML snippet and optionally the surrounding DOM. The tool returns:

Best Selector: #submitBtn

CSS Selector: div.form > button#submitBtn

XPath Selector: /html/body/div[2]/form/button[1]

Use the output directly in your automation script.
