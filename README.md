# Penny

A responsive personal finance dashboard using Lato. See your signed-in Google account, balances across your accounts and cash on hand, savings, SIP contributions, monthly and all-time spending, category spending in a pie chart, and complete payment history. The **Spending breakdown → All time** view shows month-by-month spending totals as a bar chart.

## Firebase setup

Penny uses Google sign-in with Firebase Authentication and Cloud Firestore. Each account's complete Penny data is stored in its own `users/{userId}` document. `firestore.rules` restricts reads and writes to the signed-in owner. Do not replace those rules with public read/write rules.

1. Create a Firebase project in the [Firebase console](https://console.firebase.google.com/) and register a Web app.
2. In **Authentication → Sign-in method**, enable **Google** and choose a project support email.
3. Create a **Cloud Firestore** database.
4. Copy the web app's `apiKey`, `authDomain`, `projectId`, and `appId` into `firebase-config.js`. These identify the project and are visible to browser users; Firestore rules provide the access control. Never add a service-account key to this site.
5. Publish the contents of `firestore.rules` in **Firestore Database → Rules**.
6. Add the site host (and `localhost` for local development) to **Authentication → Settings → Authorized domains**.

On first sign-in, Penny offers to import the existing browser data into that Firebase account. Signing in on another device loads the cloud copy. A local per-account cache is also kept in that browser.

## Run locally

Serve the folder over HTTP instead of opening `index.html` as a `file://` URL. For example, run `python3 -m http.server 8000` in this folder, then open `http://localhost:8000`. Add `localhost` to Firebase's authorized domains. No build step or dependency installation is needed.

## Deploy to Vercel

This is a static site: Vercel serves `index.html`, `styles.css`, `app.js`, `firebase-config.js`, `firestore.rules`, and `assets/` directly. No package installation or build step is needed.

1. Put this folder in a Git repository and push it to GitHub, GitLab, or Bitbucket.
2. In Vercel, choose **Add New → Project** and import that repository.
3. Leave the framework preset as **Other**. Leave the build command and output directory empty. If the project is inside a larger repository, set the root directory to this folder.
4. Deploy. Vercel will provide a URL; open it on your phone and use your browser’s **Add to Home Screen** option for quick access.

The included `vercel.json` enables clean URLs. Add the Vercel hostname to Firebase Authentication's authorized domains.

## Data

Payments, categories, account balances, savings, investments, and profile preferences sync to the signed-in user's Firestore document. The browser also keeps a local cache, but the cloud copy is the source loaded after sign-in. Existing browser data is offered for import the first time an account is used. The app currently displays amounts in Indian rupees. Profile settings let you set the name shown in Penny, a default payment account, a monthly spending target, and a savings goal. Use **Edit balances → Add another account** to track more bank accounts or other balances; every account can have its own name, emoji, and current balance. Added accounts are available when selecting where a payment, savings deposit, or SIP contribution comes from. Use **Set cash on hand** to record physical cash. New payments, savings deposits, and recorded SIP contributions reduce the selected account balance. Older payments remain in your spending totals but are not assigned to an account automatically.

Set your existing savings with **Set balance**, or log additions with **Add savings**. Edit the total contributed, monthly SIP amount, and funding account in **Edit investments**. After the bank debit has happened, select **Record SIP** once that month; Penny prevents a second entry for the same month. SIP totals represent contributions only, not live investment value or market returns. The app does not connect to your bank or detect the debit automatically.
