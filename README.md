# Penny

A responsive personal finance dashboard using Lato. See the combined balance across two accounts, savings, SIP contributions, monthly and all-time spending, category spending in a pie chart, and recent payments. The **Spending breakdown → All time** view shows month-by-month spending totals as a bar chart.

## Run locally

Open `index.html` in a browser. The app uses plain HTML, CSS, and JavaScript, so it does not need a build step or dependency installation.

## Deploy to Vercel

This is a static site: Vercel serves `index.html`, `styles.css`, `app.js`, and `assets/` directly. No package installation or build step is needed.

1. Put this folder in a Git repository and push it to GitHub, GitLab, or Bitbucket.
2. In Vercel, choose **Add New → Project** and import that repository.
3. Leave the framework preset as **Other**. Leave the build command and output directory empty. If the project is inside a larger repository, set the root directory to this folder.
4. Deploy. Vercel will provide a URL; open it on your phone and use your browser’s **Add to Home Screen** option for quick access.

The included `vercel.json` enables clean URLs. The app does not need environment variables or a server function.

## Data

Payments, categories, account balances, savings, and investments are saved in the browser’s local storage on the device where they were entered. They do not sync between devices and can be cleared if the browser’s site data is removed. Moving from the local `file://` page to the Vercel URL creates a separate storage space; existing local entries will not automatically transfer. The app currently displays amounts in Indian rupees. Account balances start at zero; set your current balances using **Edit balances**. New payments, savings deposits, and recorded SIP contributions reduce the selected account balance. Older payments remain in your spending totals but are not assigned to an account automatically.

Set your existing savings with **Set balance**, or log additions with **Add savings**. Configure the monthly SIP amount and funding account in **SIP settings**. After the bank debit has happened, select **Record SIP** once that month; Penny prevents a second entry for the same month. SIP totals represent contributions only, not live investment value or market returns. The app does not connect to your bank or detect the debit automatically.
