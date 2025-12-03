# Brew Portal

In this assignment, you will extend your **Brew in the Cloud** project by adding user authentication and user-specific beverage management. Each signed-in user should be able to log in, create custom beverages, and see only their own saved beverages. You will also add Firestore security rules so that users cannot access data that does not belong to them.

## Objectives

- Configure Firebase Authentication with Google Sign-In.
- Protect access to the beverage dashboard so only authenticated users can view or create beverages.
- Store user-created beverages in a way that links each document with the signed-in user.
- Load and display only beverages that belong to the current user.
- Update your Pinia store to track authentication state and to manage user-specific Firestore listeners.

---

## Getting Started

Accept your instructor’s [GitHub Classroom invitation](https://classroom.github.com/a/ojKNetjK) to create your project repository.

You may copy all needed code from your previous **Brew in the Cloud** project into this new repository.

---

### 1. Firebase Setup

1. In the Firebase Console, enable Authentication and turn on Google Sign-In.

2. Copy your Firebase configuration into the provided firebase.ts file in this project.

3. Make sure your Firebase setup works correctly so that:

   - The app initializes Firebase without errors.

   - Authentication can detect login and logout changes.

   - Your Firestore data design can support connecting beverages with the signed-in user later in the assignment. (You need to update your collection or document structure as needed in the next tasks.)

### 2. Pinia Store Updates

Update your `beverageStore.ts` so that it stores both the current user and the beverages for that user.

Your store should:

- Track:

  - `user: User | null`
  - `beverages: BeverageType[]`
  - `currentBeverage: BeverageType | null`

- Include a `setUser(user: User | null)` action that:

  - Saves the Firebase user in the store,
  - Stops the previous Firestore listener when the user changes,
  - Starts a new listener for the new user,
  - Updates beverage data when Firestore reports changes,
  - Sets `currentBeverage` correctly when the beverage list updates.

- Include a `makeBeverage()` action that:
  - Checks whether a user is signed in,
  - Checks whether all required fields are filled in,
  - Builds a unique beverage id,
  - Writes the beverage document to Firestore,
  - Updates the store state so the UI responds at once,
  - Returns a short message such as:
    - `"Beverage <name> made successfully!"`,
    - `"No user logged in, please sign in first."`,
    - `"Please complete all beverage options and the name before making a beverage."`

### 3. Google Login and Auth State

Update your `App.vue` component so the UI responds to login changes.

Your app should:

- Before the user signs in

  - Show a Sign in with Google button that calls withGoogle() when clicked, and no Sign out button.
  - The "Make Beverage" button should be disabled.
  - No saved beverages should be displayed.

- After the user signs in
  - Show the signed-in user’s name (or email).
  - Show a Sign out button, and clicking it should log the user out.
  - Load and display only the beverages that belong to the signed-in user.
  - The Make Beverage button should be available, and clicking it should create a beverage under the current signed-in user.

The `withGoogle()` function should:

- Use `GoogleAuthProvider`Sign in the user,
- Handle errors by showing a message in the UI,
- Let the Firestore listener update the store through `setUser()`.

### 4. UI and UX Requirements

Your user interface should:

- Keep all controls from the previous project:

  - Temperature selection,
  - Base selection,
  - Syrup selection,
  - Creamer selection,
  - Beverage name input,
  - The beverage preview component.

- Add authentication features:

  - Google Sign-In button,
  - A clear display of the current signed-in user,
  - A message area for login errors and success messages,
  - Use [onAuthStateChanged](https://firebase.google.com/docs/auth/web/manage-users) to monitor the current authentication state.

- Show saved beverages for the current user:
  - Use radio buttons or a simple selection interface,
  - Update the preview when the selection changes,
  - Show nothing when the user has no saved beverages.

You do not need a complex layout. A clean structure that is easy to test is enough.

---

## Expected Outcome

A working demo is available for reference:  
[Expected Outcome Demo](https://gvsu-cis371.github.io/BrewPortal/)

---

## Grading Rubric

| Grading Item | Points |
| --- | --: |
| Firebase Setup, Google Sign-In works (login button, successful login, user info appears) | 15 |
| Before login: Make Beverage button is disabled, and no beverages are shown | 15 |
| After login: beverages can be created and only the current user’s data appears | 30 |
| Login state changes behave correctly (logout clears UI, re-login loads correct beverages) | 30 |
| GitHub Clone, Commit, Push, & Deploy to GitHub Pagesl | 10 |

---

## Deliverables

- Deploy your web application using the following commands in your `terminal`:

  ```bash
   npm run build
   npm run deploy
  ```

- Github Page Setup

  - Set up your GitHub repository for GitHub Pages deployment. Follow the steps shown in the image below: ![Layout](../assets/img/project1-githubpage.jpg).
  - Your web application will be accessible at the URL: gvsu-cis371.github.io/YOUR-REPO

- Submit the URL of your GitHub Page in Blackboard.
