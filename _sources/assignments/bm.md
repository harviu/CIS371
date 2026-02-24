# Beverage Maker

— SCSS + TypeScript

In this assignment, you will build a small interactive “Beverage Maker” web app using **TypeScript** and **Sass (SCSS)**. The page includes a mug graphic and several option groups (temperature, base beverage, syrup, cream). Your job is to complete the missing SCSS mixin and finish the TypeScript functions so the UI updates correctly when the user changes options.

## Objectives

By completing this assignment, you will practice:

- SCSS Mixins: Refactor repeated styles into an SCSS mixin and reuse it with `@include`.
- DOM Events: Use `addEventListener("change", ...)` to react to radio button selection changes.
- DOM Manipulation: Update element classes and styles to reflect user choices.
- CSS Variables: Use CSS custom properties (for example `--syrup-color`) to connect TypeScript state to CSS styling.

## Best Solutions:

-
-

## Preparation

- **IDE Setup:** Use [VS Code](https://code.visualstudio.com/) for editing and managing your code.
- **Development Environment:**
  1. **NodeJS Environment Setup**: Choose one of the following options to set up your NodeJS environment,
     - Docker Container: Create a Node.js development environment with Docker. For detailed instructions, please refer to the [class slides](../assets/pdf/Docker.pdf).
     - Direct Install: Alternatively, you can install NodeJS directly from the [NodeJS official website](https://nodejs.org).

     In the context of this document, the term `terminal` refers to:
     - Command Prompt: On Windows systems.
     - Terminal: On macOS systems.
     - Shell or Bash: Inside a Docker container, depending on the base image of the container.

     Verify the installation by execute the command in `terminal`:

     ```bash
     node -v    # v14 or newer
     npm -v     # v8 or newer
     ```

  2. **GitHub Setup:**
     1. Create a [GitHub account](https://github.com) if you don't have one.
     2. Ensure you can access your GitHub account using an SSH Key. If you haven't set this up, follow the steps below or check this [tutorial](https://youtu.be/a-zX_qc2S-M).
        - Open a `terminal`. If you haven't yet configured an SSH key for GitHub on your machine, generate a new one with the following command:

          ```bash
          ssh-keygen
          ```

        - Navigate to your GitHub account settings(web). Click on `SSH and GPG keys` and then `New SSH key`. Paste the public key that was generated in the first step and click `Add SSH key`. ![github-sshkey](../assets/img/github-sshkey.png)

        - Set up your GitHub username and email in a `terminal``. You can do this with the following commands:

          ```bash
           git config --global user.name "Your Name"
           git config --global user.email "your-email@example.com"

          ```

  3. Accept your instructor's [GitHub classroom invitation](https://classroom.github.com/a/4g9uZf0N) to set up your project repository.
     1. **Select Your Name:** ![select-name](../assets/img/github-classroom-selectname.png)
     2. **Initialize Your Assignment Repository:** ![init-repo](../assets/img/github-classroom-initrepo.png)
     3. **Clone the Repository:** ![clone](../assets/img/github-classroom-sshclone.png) You're now ready to clone the repository. In your `terminal`, use the following command with your SSH repository link to download the repository to your local machine:

        ```bash
        git clone [YOUR_SSH_REPO_LINK]
        ```

     4. **Install Required Packages:** Execute the following command to install the necessary packages for your project:

        ```bash
        cd [YOUR_REPO]
        npm install
        ```

  4. Run a local development server (default port 5173):

     ```bash
     npm run dev
     ```

     Then you can access your project at `localhost:5173` in browser.

## Instructions

### Task 1: SCSS mixin in `src/style.scss`

In `src/style.scss`, you will see a `.syrup` style block that contains a repeating linear gradient with a hard-coded color (for example `#ffefd5`).

Refactor this syrup styling into a mixin:

- Create an SCSS mixin named `syrup-layer`.
- The mixin must accept one parameter: the stripe color (for example `$color`).
- Replace the hard-coded color in the gradient with `$color`.
- Update `.syrup` to use the mixin via `@include`.

Goal: changing the syrup stripe color should require changing only one argument, without copying the gradient code.

### Task 2: Syrup behavior in `src/main.ts`

Complete the following functions:

```ts
function applySyrup(input: HTMLInputElement): void {
  // TODO: implement this function
}

function setupSyrupListeners(): void {
  // TODO: implement this function
}

setupSyrupListeners();
```

**`applySyrup` behavior:**

- When the user selects a syrup option, update the syrup layer in the mug.
- Use the `syrups` color map (provided in starter code) to look up the selected syrup color.
- Set CSS variable `--syrup-color` on the `.syrup` element so SCSS can use it. For how to set a CSS variable in JavaScript, please refer to the following documentation: [https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Cascading_variables/Using_custom_properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Cascading_variables/Using_custom_properties)

**`setupSyrupListeners` requirements:**

- Add `"change"` event listeners to all syrup radios: `input[name="syrup"]`.
- On page load, apply the initial syrup state using the currently checked radio.

### Task 3: Temperature, cream, and base behavior in `src/main.ts`

Complete the following functions:

```ts
function setupCreamListeners(): void {
  // TODO: implement this function
}
setupCreamListeners();

function setupTemperatureListeners(): void {
  // TODO: implement this function
}
setupTemperatureListeners();

function setupBaseListeners(): void {
  // TODO: implement this function
}
setupBaseListeners();
```

Required behavior:

#### Temperature

- Add `"change"` listeners to `input[name="temperature"]`.
- When a temperature radio changes, call the provided `applyTemperature(input)` function.
- On page load, call `applyTemperature()` once using the currently checked temperature radio.

#### Cream

- Add `"change"` listeners to `input[name="cream"]`.
- When a cream radio changes, call the provided `applyCream(input)` function.
- On page load, call `applyCream()` once using the currently checked cream radio.

#### Base beverage

- Add `"change"` listeners to `input[name="base"]`.
- When a base radio changes, call the provided `applyBase(input)` function.
- On page load, call `applyBase()` once using the currently checked base radio.

#### Expected Outcome

- [Expected Outcome Demo](https://gvsu-cis371.github.io/BeverageMaker/)

## Grading Rubric

| Category                                                |  Points |
| ------------------------------------------------------- | ------: |
| GitHub setup, commits, push, & GitHub Pages deployment  |      15 |
| Task 1: SCSS mixin (syrup-layer) in src/style.scss      |      25 |
| Task 2: Syrup functions in src/main.ts                  |      25 |
| Task 3: Cream + Temperature + Base listeners in main.ts |      25 |
| Code quality & organization                             |      10 |
| **Total**                                               | **100** |

## Deliverables

- Deploy your web application using the following commands in your `terminal`:

  ```bash
   npm run build
   npm run deploy
  ```

- Github Page Setup
  - Set up your GitHub repository for GitHub Pages deployment. Follow the steps shown in the image below: ![Layout](../assets/img/github-page.png).
  - Your web application will be accessible at the URL: gvsu-cis658.github.io/YOUR-REPO

- Submit the URL of your GitHub Page in Blackboard.
