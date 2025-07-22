# JS Unit Testing

## Learning Objectives

- [ ] Understand what unit testing is and how it relates to other testing methods
- [ ] Know how to write a unit test that checks the output of a function
- [ ] Understand what Test Driven Development is and how it is used
- [ ] Know how to run unit tests locally (via the command line)

---

## What are unit tests

When developing apps, errors inevitably emerge in your code. That's why apps must be tested
regularly to ensure that they work as expected. Since manual testing by clicking in the UI is very
time consuming and cumbersome, tests are automated.

Test automation can be performed in several ways. A good classification is provided by the
[Testing Trophy](https://kentcdodds.com/blog/the-testing-trophy-and-testing-classifications).

Static Testing refers to linting and can be understood as a spell checker for your code.

Unit tests check whether a single function works as intended. The goal is to test each individual unit
independently and isolated from other data and external influences. The test can be run
automatically after each modification to ensure latest changes won't break the app.

---

## Test Driven Development (TDD)

With Test driven development (TTD) the test is written first. Afterwards you write the function,
which should create a desired result.

Following this approach you get feedback as early as possible whether your work is going into the
right direction. In the beginning all tests will fail. Gradually more and more test will be
successful. The implementation of your function is finished as soon as all test runs are successful.

---

## How to test with jest

Tests are placed in a file next to the code you like to test, but with `.test.js` as filename
ending.

```
calculator.js			<--- Code used in your app
calculator.test.js		<--- Tests for this code
```

When writing tests, you build various different scenarios that check a certain desired result of a
function. Each of such test cases is wrapped into a function called
[test()](https://jestjs.io/docs/api#testname-fn-timeout). The first argument of the `test()`
function is a description of the test case in plain english.

Unit tests usually have a similar structure. First, the function to be tested is called and any
required arguments are passed. Afterwards the result of this function call is passed to the
[expect()](https://jestjs.io/docs/expect) function. Thus different
[matcher](https://jestjs.io/docs/using-matchers) functions like `toBe()` or `toEqual()` can be used.

This way the actually generated result of the function is checked against an expected result defined
in the test case.

```js
import { add } from "calculator";

test("adds the numbers 1, 2 and 3 correctly", () => {
  const result = add(1, 2, 3);
  expect(result).toBe(6);
});

test("adds the numbers 13, 28 and 42 correctly", () => {
  const result = add(13, 28, 42);
  expect(result).toBe(83);
});
```

---

## Run Tests locally

Run all tests:

```sh
npm run test
```

When executing this commands you will see the result of the test run: a list of all included tests
and whether they were successful or failed.

---

## Resources

- [Jest](https://jestjs.io/)
- [Testing Trophy and Testing Classifications](https://kentcdodds.com/blog/the-testing-trophy-and-testing-classifications)
Handout:
https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/js-unit-testing/js-unit-testing.md?plain=1

-------------------------------------------------------------------------------------------------------------------
# React Component Testing

## Learning Objectives

- [ ] Understanding the idea of component testing
- [ ] Knowing how to
  - render a React component in tests
  - simulate interaction with a rendered React component in tests
  - searching for expected elements in the rendered React component
  - formulate expected results
- [ ] Having a general understanding of mocks

---

## Why Testing Frontend makes sense

When developing apps we have to test them on a regular basis to ensure everything works as expected and to find bugs before users do.

Manually testing the app by using the UI is time consuming and unreliable. Rendering a part of UI and simulating interactions can be automated in component tests.

This approach tries to interact with the app in the same way a real user would, by searching in the rendered app for certain elements:

- Search for a heading with certain content
- Search input fields with certain labels and insert text
- Search for a button with a certain label and click to submit a form
- Search for an expected result that should be displayed after submit

We can write such tests for each React component in our code.

In a previous session we looked at unit testing, which is concerned with a single unit / function. Component testing falls in the category of integration tests, because it tests how various individual units / functions work together to create a result on user's screens.

Instead of testing the full app or a complete page (this approach would be End-to-End Testing), we create separated smaller tests for individual components.

We place the file including the tests directly besides the component file with the ending `.test.js`.

```
MyComponent
├── MyComponent.styled.js
├── MyComponent.test.js
└── index.js
```

---

## Testing Library

The [Testing Library](https://testing-library.com/docs/react-testing-library/intro) enables us to render React components in jest tests, simulate user behavior and check the results after re-rendering the component.

### Example

##### FahrenheitConverter.js

The component `FahrenheitConverter` renders a heading, a form and result output. If the form has not been submitted yet, a fallback message will be displayed instead of the result. After the form has been submitted the calculation is done and the result is saved in state. This will trigger a re-rendering of the component, so that the result will be displayed.

```jsx
import { useState } from "react";

export default function FahrenheitConverter() {
  const [fahrenheit, setFahrenheit] = useState();

  function handleSubmit(event) {
    event.preventDefault();

    const form = event.target;
    const formElements = form.elements;
    const celsius = formElements.celsius.value;

    setFahrenheit((celsius * 9) / 5 + 32);
  }

  return (
    <div>
      <h1>Temperature Unit Converter</h1>
      <form onSubmit={handleSubmit}>
        <label htmlFor="celsius">°C</label>
        <input type="number" id="celsius" name="celsius" />
        <button>Convert to Fahrenheit</button>
      </form>
      {fahrenheit ? (
        <output>{fahrenheit} °F</output>
      ) : (
        <p>Please enter a Celsius value and submit</p>
      )}
    </div>
  );
}
```

##### FahrenheitConverter.test.js

There are three tests for this component:

1. Test that the heading is displayed
2. Test that the fallback message is displayed before the form has been submitted
3. Test that the form interaction and submit works and the result is calculated correctly and displayed instead of the fallback message.

```jsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import FahrenheitConverter from ".";

test("renders a heading", () => {
  render(<TemperatureUnitConverter />);
  const heading = screen.getByRole("heading", {
    name: /temperature unit converter/i,
  });
  expect(heading).toBeInTheDocument();
});

test("renders a fallback message if form is not yet submitted", () => {
  render(<FahrenheitConverter />);
  const message = screen.getByText(/please enter a celsius value and submit/i);
  expect(message).toBeInTheDocument();
});

test("converts Celsius to Fahrenheit and renders the result", async () => {
  const user = userEvent.setup();

  render(<FahrenheitConverter />);

  const input = screen.getByLabelText(/°C/i);
  expect(input).toBeInTheDocument();

  const button = screen.getByRole("button", { name: /convert to fahrenheit/i });
  expect(button).toBeInTheDocument();

  await user.type(input, "5");
  await user.click(button);

  const output = screen.getByText(/41 °F/i);
  expect(output).toBeInTheDocument();

  const message = screen.queryByText(
    /please enter a celsius value and submit/i
  );
  expect(message).not.toBeInTheDocument();
});
```

### Rendering a component

With the [`render`](https://testing-library.com/docs/react-testing-library/api#render) method you can render the `FahrenheitConverter` component initially. Afterwards you can use the [`screen`](https://testing-library.com/docs/queries/about/#screen) method to access the HTML generated by the component.

### Using Queries

With [`screen`](https://testing-library.com/docs/queries/about/#screen) you can use [queries](https://testing-library.com/docs/queries/about) to search for specific elements you expect to be in the generated HTML.

| Query                                                                 | Description                                                                                                                   |
| --------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| [`ByRole`](https://testing-library.com/docs/queries/byrole)           | Search for an element based on their `role` / `aria-*` attribute (for example `button`, `textbox`, `heading`)                 |
| [`ByLabelText`](https://testing-library.com/docs/queries/bylabeltext) | Search for an element (like an input field) with a given label                                                                |
| [`ByText`](`https://testing-library.com/docs/queries/bytext`)         | Search for a given text                                                                                                       |
| [`ByTestId`](https://testing-library.com/docs/queries/bytestid)       | Last resort to search for an element you can't address with other queries. Mark the element with the attribute `data-testid`. |

In most cases you should use queries with `getBy` to immediately fail when the element is not found. Sometimes you like to test whether something is _not_ displayed. Use `queryBy` in this case because it doesn't immediately fail the test but returns `null`.

You can use a string to define a text to search for, like: `getByText("Text Here")`.

You can also place the text in slashes followed by an `i` _instead of_ double quotes for a string, like `getByText(/text here/i)`

This makes your tests more resilient to changes in the implementation: `getByText("Text here")` would start to fail if the component were to change the casing. Because of this, this is a very common convention when writing tests. Even though `/text here/i` may look funny at first, you'll get used to it rather quickly.

The literal expression enclosed in slashes (`/hello world/`) is called a [regular expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions). The `i` modifier at the end tells the regular expression to ignore lower- and uppercase differences. Regular expressions are often used for searching things in large strings and are very powerful. You don't need to dive into them any deeper than shown above to write your tests though.

Using the [Testing Playground](https://testing-playground.com/) will help you to write queries.

### Simulate user events

You can [simulate how users interact](https://testing-library.com/docs/user-event/intro) with the component. First you need to setup a virtual user with `userEvent.setup()`. Then you can simulate events like `type` or `click`. Don't forget to use `await` with user events.

### Using Matchers

With [`expect`](https://jestjs.io/docs/expect) you can use [matchers](https://jestjs.io/docs/using-matchers) to formulate an expected result of your test: It's the same concept for unit testing.

Since we are generating HTML in component tests, you can use some [additional matchers](https://github.com/testing-library/jest-dom#custom-matchers). The `toBeInTheDocument` matcher is used very commonly.

---

## Mocks

[A mock](https://jestjs.io/docs/mock-functions) is a substitute that is used in the tests instead of an original function. Common use cases are:

- Event-handler functions passed as prop to a component
- Replacing an imported package

Mocks are used to reduce dependencies in a test and to provide a testable environment for a component.

### Mock Function for Event-Handlers

Consider a `Counter` component that accepts two event-handler functions as prop:

```jsx
export default function Counter({ onDecrease, onIncrease }) {
  return (
    <>
      <button type="button" onClick={onDecrease}>
        decrease
      </button>
      <button type="button" onClick={onIncrease}>
        increase
      </button>
    </>
  );
}
```

In a test you might want to test if the passed event-handler functions are called when the buttons are clicked. Since you are not rendering a complete app in the test, but only this component, you can pass a mock function.

Mock function can be created with `jest.fn()`. This gives you a function you can use with `expect`.

```jsx
test("should call event-handler functions", async () => {
  // Creates mock functions
  const handleDecrease = jest.fn();
  const handleIncrease = jest.fn();

  const user = userEvent.setup();

  render(<Counter onDecrease={handleDecrease} onIncrease={handleIncrease} />);

  const decreaseButton = screen.getByRole("button", {
    name: /decrease/i,
  });
  const increaseButton = screen.getByRole("button", {
    name: /increase/i,
  });

  await user.click(increaseButton);
  await user.click(decreaseButton);
  await user.click(increaseButton);

  expect(handleDecrease).toHaveBeenCalledTimes(1);
  expect(handleIncrease).toHaveBeenCalledTimes(2);
});
```

### Testing Next.js (`useRouter` Mock)

When writing tests for components that use the `useRouter` hook from Next.js, you need to be aware of some stumbling stones. When tests are executed they don't run within a real browser. Thus there is no [browser location API](https://developer.mozilla.org/en-US/docs/Web/API/Location) and the context that Next.js uses to provide routing information to all components in the app is not present.

The `useRouter` hook requires the browser location API to work, so it will throw an error and fail the tests.

In order to test components including the `useRouter` hook, you need to write a mock.

A mock is a substitute that is used in the tests instead of the original function. You can replace the `useRouter` hook from `next/router` with a mock like described below. Add the functions / properties of the router that the tested component uses. In a mock, use the simplest possible implementation that makes the tests work. In the following example we assume that the tested components accesses `router.asPath` and calls `router.push`.

```jsx
import MyComponent from ".";
/* ... likely more imports here ... */

jest.mock("next/router", () => ({
  useRouter() {
    return {
      push: jest.fn(),
      asPath: "/",
    };
  },
}));

test("should render", () => {
  /* ... test here ... */
});

/* ... likely more tests here ... */
```

---

## Resources

- [Testing Library](https://testing-library.com/docs/react-testing-library/intro/)
- [Testing Library: render](https://testing-library.com/docs/react-testing-library/api#render)
- [Testing Library: screen](https://testing-library.com/docs/queries/about/#screen)
- [Testing Library: Queries](https://testing-library.com/docs/queries/about/)
- [Testing Playground](https://testing-playground.com/)
- [Testing Library: UserEvents](https://testing-library.com/docs/user-event/intro)
- [jest-dom (additional matchers)](https://github.com/testing-library/jest-dom)
- [Jest: Mock functions](https://jestjs.io/docs/mock-functions)

- Handout:
  https://github.com/neuefische/allspice-cgn-fssd-25/blob/main/sessions/react-component-testing/react-component-testing.md?plain=1
  
-------------------------------------------------------------------------------------------------------------------
