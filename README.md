# Exercise SAREVIA: free self-hosted setup

This package runs the exercise on your own web address at no cost. It uses two free services:

- **Firebase (Spark plan)** for sign-in, the live clock, messages and team answers. The Spark plan needs no credit card and cannot create a bill: if a limit is reached, it pauses until the next day.
- **GitHub Pages** to host the page itself.

Setup takes about 30 minutes, once.

## What is in the package

| File | Where it goes |
|---|---|
| `site/index.html` | Your website (the exercise) |
| `site/firebase-config.js` | Your website (your Firebase settings go here) |
| `firestore.rules` | Pasted into Firebase (who can see what) |
| `sample-messages.json` | Kept on your computer, imported in the facilitator console. **Never upload it to the website**, or participants could read the messages in advance. |

## Step 1. Create the Firebase project

1. Go to https://console.firebase.google.com and sign in with a Google account.
2. Click **Create a project**, give it a name (for example `sarevia-exercise`), and finish the wizard. You can turn Google Analytics off.
3. Stay on the free **Spark** plan. Do not upgrade to Blaze.

## Step 2. Turn on sign-in

1. In the left menu, open **Build > Authentication** and click **Get started**.
2. On the **Sign-in method** tab, enable **Email/Password**.
3. On the **Users** tab, click **Add user** and create a facilitator account with an email and a password. Repeat for each co-facilitator.

Team logins are created later from the facilitator console, so you don’t add them here. Anonymous sign-in is not used; if you turned it on for an earlier version, you can turn it off.

## Step 3. Create the database and paste the rules

1. Open **Build > Firestore Database** and click **Create database**.
2. Choose a location close to you (for example `europe-west3` Frankfurt) and **Start in production mode**.
3. Open the **Rules** tab. Replace everything with the contents of `firestore.rules`.
4. In the rules, replace `facilitator@example.org` with your facilitator email addresses, in lower case, separated by commas:
   `'trainer1@example.org', 'trainer2@example.org'`
5. Click **Publish**.

## Step 4. Connect the page to your project

1. In Firebase, click the gear icon > **Project settings**.
2. Under **Your apps**, click the web icon (`</>`), give the app a nickname, and register it. You do not need Firebase Hosting.
3. Firebase shows a block of settings starting with `const firebaseConfig = {`. Copy the values between the braces.
4. Open `site/firebase-config.js` in a text editor and replace the placeholder values with yours. Save the file.

These settings are not secret: they only identify your project. Security comes from the rules in step 3.

## Step 5. Publish the site on GitHub Pages

1. Create a free account at https://github.com.
2. Click **New repository**, name it (for example `sarevia`), set it to **Public**, and create it.
3. Click **uploading an existing file** and drag in the two files from the `site` folder: `index.html` and `firebase-config.js`. Click **Commit changes**.
4. Open **Settings > Pages**. Under **Branch**, choose `main` and `/ (root)`, then **Save**.
5. After a minute or two, your address appears at the top of that page, for example `https://yourname.github.io/sarevia/`.
6. Back in Firebase, open **Authentication > Settings > Authorized domains** and add `yourname.github.io`.

To use your own domain instead (for example `exercise.yourdomain.org`), enter it under **Settings > Pages > Custom domain** and follow GitHub’s DNS instructions, then add that domain to Firebase’s authorized domains too.

**Updating from an earlier version of this package:** upload the new `index.html` to GitHub, replacing the old one, and paste the new `firestore.rules` into Firebase (keeping your facilitator emails). Your `firebase-config.js` stays as it is.

**Optional, to install as an app:** also upload `manifest.webmanifest`, `icon-192.png`, `icon-512.png` and `apple-touch-icon.png` from the `site` folder, next to `index.html`. See “Open it like an app” below.

## Step 6. Load the messages

1. Open your site and click **Facilitator sign-in** at the bottom of the page.
2. Sign in with the facilitator account from step 2.
3. Open the **Facilitator** tab, click **Import messages**, and choose `sample-messages.json`.
4. Edit the texts and minutes as you like, then click **Save messages**.

## Running a session

1. **Create the team logins.** In the Facilitator tab, under **Team logins**, enter how many teams you need (for example 4) and a name (for example “Group”), then click **Create team logins**. Each team gets a name, a login and a password. You can rename teams in the table; names must be unique.
2. **Hand them out.** Click **Download login cards (PDF)** and print or share one card per team, or use **Copy login list**. Every member of a team can sign in with the same login on their own device. They all see and edit the same answers, which update live.
3. Open the site yourself, sign in with your email, and keep the Facilitator tab open throughout. Scheduled messages are sent from your page.
4. Click **Start exercise**. You can pause, add five minutes, send any message early with **Send now**, and watch every team’s progress in the Teams table.
5. At the end, export the results, then **Clear team answers** and **Reset exercise**. Before the next group, click **New passwords for all** so the previous participants can’t sign back in, and print new login cards. **Delete** removes a team’s login entirely.

Team passwords are kept in the facilitator-only part of the database so you can reprint cards. They are training passwords: don’t reuse them anywhere else.

## Rating teams and exporting results

1. **Teams submit.** On the Decision brief tab, each team clicks **Submit final answers**. Their answers lock, and the Teams table shows “Submitted” with the time and how many teams are done. Use **Reopen** to unlock a team that needs to change something.
2. **Set the scoring key.** In each message, choose the **Best option** and, if you like, one **Also acceptable** option, then save. These stay hidden from teams. The sample messages already have them set.
3. **Rate each team.** Click **Rate** next to a team. You see all its answers with your facilitator notes, and give each written section a score from 0 (not done) to 5 (excellent), with an optional comment and an overall comment. Ratings save automatically.
4. **Automatic scores.** Option choices score 5 for the best option, 3 for an acceptable one and 0 otherwise. The asset allocation starts at 5 and loses 2 points per error and 1 per warning from the plan checks.
5. **Export.** Click **Export results as PDF**. The report has a ranking of all teams, the messages sent with their scoring key, and one page per team with every score and comment. Untick “Include each team’s full answers” for a shorter report.

The percentage counts only the sections you have rated, so rate every section before exporting the final report. The ranking shows how many sections are still unrated for each team.

Use **Export messages** to keep a copy of each scenario, and **Import messages** to switch between them.

## Open it like an app

Once the site is installed, it opens in its own window with the SAREVIA icon and no address bar.

- **Windows or Mac, Chrome or Edge:** open the site, click the install icon at the right end of the address bar (a monitor with a down arrow), or open the ⋮ / … menu and choose **Install SAREVIA** (in Edge: **Apps > Install this site as an app**). It then appears in the Start menu, Dock or Launchpad, and on the desktop if you choose.
- **Android, Chrome:** open the site, tap ⋮ and choose **Install app** or **Add to home screen**.
- **iPhone or iPad, Safari:** open the site, tap the Share button and choose **Add to Home Screen**.
- **Firefox and Safari on Mac** can’t install sites the same way. On a Mac, Safari can: **File > Add to Dock**.

The installed app is the same website, so updates you upload to GitHub appear in it automatically.

## Free limits in practice

The Spark plan allows 20,000 database writes and 50,000 reads per day. Answers save every few seconds while a team types, so a session with up to about 20 teams fits comfortably. For several large sessions on the same day, spread them across two Firebase projects.

## Troubleshooting

- **“Setup needed” banner:** `firebase-config.js` still has placeholder values, or was not uploaded next to `index.html`.
- **Sign-in fails for everyone:** Email/Password sign-in is not enabled (step 2), or the site’s domain is missing from Authorized domains (step 5).
- **Signed in but no Facilitator tab:** the email in the rules does not exactly match the account, or the rules were not published (step 3).
- **“Login or password is incorrect” for a team:** check the card, or give that team a **New password**. Logins are lower case and have no spaces.
- **Team signs in but sees “isn’t a team login”, or answers don’t save:** the rules from step 3 are out of date. Paste the current `firestore.rules` again (keeping your facilitator emails) and publish.
- **Creating team logins fails:** make sure **Email/Password** sign-in is enabled (step 2). Firebase also limits how many accounts can be created per hour from one connection; if you hit it, wait an hour.
- **Teams don’t receive messages:** the facilitator page was closed or the clock is paused. Use **Send now**.
