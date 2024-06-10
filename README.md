# @storybook/test-runner

Storybook test runner turns all of your stories into executable tests. It is powered by Jest and Playwright.

- For those without a play function: it verifies whether the story renders without any errors.
- For those with a play function: it also checks for errors in the play function and that all assertions passed.

  - Storybook's play functions are small code snippets that run once the story finishes rendering. Aided by the addon-interactions, it allows you to build component interactions and test scenarios that were impossible without user intervention. For example, if you were working on a registration form and wanted to validate it, you could write the following story with the play function:

```ts
import type { Meta, StoryObj } from '@storybook/your-react';

// Import utility functions from '@storybook/test' for user interactions
import { userEvent, within } from '@storybook/testing-library';

// Import the component to be tested
import { RegistrationForm } from './RegistrationForm';

// Define metadata for the story, which specifies the component being documented
const meta = {
component: RegistrationForm,
} satisfies Meta<typeof RegistrationForm>;

export default meta; // Export the metadata so Storybook recognizes it

// Define a type alias for StoryObj using the meta object type
type Story = StoryObj<typeof meta>;

/\*

- Visit the Storybook documentation to understand more about using the canvasElement
- for querying the DOM within the play function:
- https://storybook.js.org/docs/writing-stories/play-function#working-with-the-canvas
  \*/
  export const FilledForm: Story = {
  // The play function allows for interaction simulation within the story
  play: async ({ canvasElement }) => {
  // Use the 'within' utility to create a scoped query function for the provided canvas element
  const canvas = within(canvasElement);

      // Retrieve the email input field using its label, specifying 'input' as the selector
      const emailInput = canvas.getByLabelText('email', {
        selector: 'input',
      });

      // Simulate typing into the email input field with a delay between keystrokes
      await userEvent.type(emailInput, 'example-email@email.com', {
        delay: 100,
      });

      // Retrieve the password input field using its label, specifying 'input' as the selector
      const passwordInput = canvas.getByLabelText('password', {
        selector: 'input',
      });

      // Simulate typing into the password input field with a delay between keystrokes
      await userEvent.type(passwordInput, 'ExamplePassword', {
        delay: 100,
      });

      /*
       * Visit the Storybook documentation to understand more about logging actions
       * automatically in the Actions panel:
       * https://storybook.js.org/docs/essentials/actions#automatically-matching-args
       */
      // Retrieve the submit button using its role
      const submitButton = canvas.getByRole('button');

      // Simulate a click event on the submit button
      await userEvent.click(submitButton);

  },
  };
```

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

More info @ https://storybook.js.org/docs/writing-tests/test-runner
