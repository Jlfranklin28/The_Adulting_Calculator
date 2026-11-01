# The Adulting Calculator: phone app

This folder turns The Adulting Calculator into a real Android and iPhone app, and a free website.
Everything the app needs is in `www/index.html`, so once installed it works with no internet.
Budgets, goals, saved scenarios and the calendar are stored on the phone.

In the installed app:
- **Export spreadsheet** opens the phone's share sheet, so the Excel file can be texted, emailed or saved.
- **Add all to my phone's calendar** sends your bills, paydays and goals to the phone's calendar.
- **Turn on phone reminders** (in the Budget calendar) sends alerts at 9 AM on the day,
  plus 9 AM the day before a bill is due.

---

## Android (free, no installs on your PC)

GitHub's free build servers make the app for you. You only need a web browser.

1. **Make a free GitHub account** at github.com, if you don't have one.
2. **Create a repository:** click **+** (top right) > **New repository**. Name it `adulting-calculator`.
   Choose **Public** if you want anyone to be able to download the app, or **Private** if it's just for you.
   Click **Create repository**.
   Then turn on the website: click **Settings** (top of the repository) > **Pages**, and under
   **Build and deployment > Source** choose **GitHub Actions**. That's all; there's nothing to save.
3. **Upload this folder:** on the new repository page, click **uploading an existing file**.
   Unzip `adulting-calculator-app.zip` on your PC, open the `adulting-calculator-app` folder,
   select everything inside it (including the `.github` folder) and drag it onto the page.
   Click **Commit changes**.
4. **Wait about 5 minutes.** Click the **Actions** tab. Two jobs run:
   "Build Android app" and "Publish website". Green checks mean they're done.
5. **Install it on your phone:** open your repository's **Releases** page on your Android phone
   (the link is on the right side of the repository page), tap `The-Adulting-Calculator.apk`,
   then tap the downloaded file. If the phone asks, allow your browser to "install unknown apps".

To share it, send people the link to the Releases page (Public repositories only).

The name under the icon is set by `appName` in `capacitor.config.json`. Some Android phones shorten
long names under the icon (for example "The Adulting..."); the full name still shows in the app and the store.
To update the app, upload a new `www/index.html` the same way; a fresh build starts on its own.

> If the `.github` folder doesn't upload by dragging, click **Add file > Create new file**,
> type `.github/workflows/android.yml` as the name, paste in the contents of that file, and commit.
> Do the same for `.github/workflows/website.yml`.

**Google Play Store:** needs a Google Play developer account ($25 one time) and a signed
release build. Ask Claude to set that up when you're ready. Decide on the app ID first
(`appId` in `capacitor.config.json`, now `com.adultingcalculator.app`), because it can't change
after the app is published.

---

## Website (free, no domain or server needed)

The same upload also puts the calculator online at:

    https://YOUR-USERNAME.github.io/adulting-calculator/

Share that link with anyone. It works on any phone or computer, keeps working offline after the
first visit, and people can add it to their home screen with the app icon
(iPhone: Safari > Share > Add to Home Screen; Android: Chrome > menu > Add to Home screen / Install app).
Every time you upload a new `www/index.html`, the website updates too.

If "Publish website" shows a red X, the Pages setting from step 2 was missed: turn it on,
then on the **Actions** tab open "Publish website" and click **Re-run all jobs**.

**Your own domain (optional):** buy a name like `adultingcalculator.com` from any domain seller,
then in **Settings > Pages > Custom domain** type it in and follow GitHub's instructions for the
DNS records. GitHub adds the secure padlock (https) for free.

---

## iPhone (needs an Apple Developer account)

Apple only lets iPhone apps be built on a Mac and installed through its own systems,
so this route needs:
- The **Apple Developer Program**, $99 per year (developer.apple.com/programs).
- **Codemagic** (codemagic.io), a service with cloud Macs. Its free plan includes 500 build minutes a month.

Steps, once you have the Apple account:
1. Upload this folder to GitHub (Android steps 1 to 3).
2. In **App Store Connect** (appstoreconnect.apple.com), create a new app with the bundle ID
   `com.adultingcalculator.app`, then go to **Users and Access > Integrations** and create an API key.
3. Sign in to Codemagic with GitHub and add the `adulting-calculator` repository.
4. In Codemagic, go to **Team settings > Integrations > Developer Portal**, add the API key,
   and name it exactly `Adulting Calculator key`.
5. Start the **iPhone app (TestFlight)** build. When it finishes, the app appears in **TestFlight**.
   Install the free TestFlight app on your iPhone to download it, and invite family by email
   from App Store Connect. From there you can also submit it to the App Store.

---

## Building on your own computer instead

**Android on Windows:** install Node.js (nodejs.org) and Android Studio, then in this folder run:

    npm install
    npx cap add android
    npm run icons
    npx cap sync android
    npm run android

Android Studio opens. Press the green Run button with your phone plugged in,
or use **Build > Build App Bundle(s) / APK(s) > Build APK(s)**.

**iPhone on a Mac:** install Xcode, then run the same commands with `ios` in place of `android`.

## Updating
Replace `www/index.html` with the newest version of the calculator, then rebuild.
