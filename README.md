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
3. Enable **Anonymous** as well. Participants join this way, without creating accounts.
4. On the **Users** tab, click **Add user** and create a facilitator account with an email and a password. Repeat for each co-facilitator.

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

**Updating from an earlier version of this package:** paste the new `firestore.rules` into Firebase (keeping your facilitator emails) and upload the new `index.html` to GitHub, replacing the old one. Your `firebase-config.js` stays as it is.

## Step 6. Load the messages

1. Open your site and click **Facilitator sign-in** at the bottom of the page.
2. Sign in with the facilitator account from step 2.
3. Open the **Facilitator** tab, click **Import messages**, and choose `sample-messages.json`.
4. Edit the texts and minutes as you like, then click **Save messages**.

## Running a session

1. Send participants the site address. Each team opens it on one device, types a team name and clicks **Create team**. No account is needed. Names must be unique: “Team Blue” and “team blue” count as the same name, and a team that picks a taken name is asked to choose another. Teams can rename themselves later with **Rename**.
2. Open the site yourself, sign in, and keep the Facilitator tab open throughout. Scheduled messages are sent from your page.
3. Click **Start exercise**. You can pause, add five minutes, send any message early with **Send now**, and watch every team’s progress in the Teams table.
4. At the end, use **Copy all debriefs**, then **Clear team answers** and **Reset exercise** before the next group. Clearing also frees all team names, and any device still open from the previous group starts fresh when reloaded.

Use **Export messages** to keep a copy of each scenario, and **Import messages** to switch between them.

## Free limits in practice

The Spark plan allows 20,000 database writes and 50,000 reads per day. Answers save every few seconds while a team types, so a session with up to about 20 teams fits comfortably. For several large sessions on the same day, spread them across two Firebase projects.

## Troubleshooting

- **“Setup needed” banner:** `firebase-config.js` still has placeholder values, or was not uploaded next to `index.html`.
- **“Couldn’t connect” banner:** Anonymous sign-in is not enabled (step 2), or the site’s domain is missing from Authorized domains (step 5).
- **Signed in but no Facilitator tab:** the email in the rules does not exactly match the account, or the rules were not published (step 3).
- **“Couldn’t create the team”:** the rules from step 3 are out of date. Paste the current `firestore.rules` again and publish.
- **Teams don’t receive messages:** the facilitator page was closed or the clock is paused. Use **Send now**.
