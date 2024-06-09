# @storybook/test-runner

Storybook test runner turns all of your stories into executable tests. It is powered by Jest and Playwright.

- For those without a play function: it verifies whether the story renders without any errors.
- For those with a play function: it also checks for errors in the play function and that all assertions passed.

## Key Features

- Comprehensive Testing: Provides a thorough testing solution by running end-to-end tests in real browser environments.
- Cross-Browser Compatibility: Ensures your components function correctly across different browsers.
- Enhanced Automation: Facilitates automated testing workflows, making it easier to catch regressions.

## How to start

Start your Storybook in terminal with:

```sh
yarn storybook
```

Open a new terminal window and run the test-runner with:

```sh
yarn test-storybook
```

The tests will automatically execute over all of your stories, and show additional information about the process.

