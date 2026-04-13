# Facebook Account Reporter — CLI Tool

A standalone CLI tool for reporting Facebook accounts and groups. Supports managing multiple Facebook accounts, fetching UIDs from profile URLs, and running concurrent reports.

## Prerequisites & Installation

1. **Install Node.js**: Ensure you have Node.js installed on your computer.
2. **Download or Clone the Project**.
3. **Install Dependencies**: Open a terminal in the project directory and run:
   ```bash
   npm install
   ```

## Termux Installation & Setup (Android)

If you are using an Android phone, you can run this tool entirely inside **Termux**. Follow these exact steps:

1. **Install Termux**: Download it from [F-Droid](https://f-droid.org/packages/com.termux/) *(Do not use the Google Play Store version as it is outdated)*.
2. **Update Packages & Install Dependencies**:
   Open Termux and run the following commands:
   ```bash
   pkg update -y && pkg upgrade -y
   pkg install nodejs -y
   pkg install unzip -y
   ```
3. **Grant Storage Permission**:
   ```bash
   termux-setup-storage
   ```
   *(A popup will appear asking for storage access. Tap "Allow".)*
4. **Extract and Setup the Tool**:
   Assuming you downloaded `massreport.zip` to your phone's default Downloads folder, run:
   ```bash
   # Copy the zip from your Downloads folder to the Termux home directory
   cp ~/storage/downloads/massreport.zip ~/
   
   # Unzip the folder
   unzip massreport.zip -d massreport
   
   # Navigate into the extracted folder
   cd massreport
   
   # Install required Node.js libraries
   npm install
   ```
5. **Run the Tool**:
   ```bash
   node cli.js
   ```

## How to Get Facebook Cookies (Kiwi Browser)

To log into your Facebook accounts securely, you'll need your session cookies.
We recommend using the **Kaguya Extension** on mobile (Kiwi Browser) or desktop.

1. **Install Kiwi Browser**: Download and install [Kiwi Browser](https://play.google.com/store/apps/details?id=com.kiwibrowser.browser) on your Android device (or use a normal browser on PC).
2. **Download Kaguya Extension**: Download the extension zip file from here: [KaguyaExtension-master.zip](https://github.com/ttkienn/KaguyaExtension/releases/download/Kaguya/KaguyaExtension-master.zip).
3. **Install Extension**:
   - Open Kiwi Browser, tap the three dots menu, and go to **Extensions**.
   - Enable **Developer mode** (toggle in the top right).
   - Tap **+(from .zip/.crx/.user.js)** and select the downloaded `KaguyaExtension-master.zip` file.
4. **Get Your Cookies**:
   - Go to [Facebook](https://www.facebook.com) and log into your account.
   - Open the Kiwi Browser menu, scroll down to the bottom, and tap on **Kaguya**.
   - Your cookies will be displayed. Copy the entire cookie string or JSON array.

## Running the Tool

Start the interactive CLI by running:
```bash
node cli.js
```

### Adding Your Accounts

1. Open the tool (`node cli.js`).
2. Select **[1] Manage Accounts**.
3. Select **[1] Add account (paste cookies)**.
4. Paste the cookies you copied from the Kaguya extension.
5. Provide a name for the account. The tool will validate the login and save it securely in the `accounts/` directory.

*Note: You can add as many accounts as you want. By adding multiple accounts, you can run batch reports on a single target.*

### Getting a Facebook UID

If you only have a profile link (e.g., `https://www.facebook.com/zuck`), you need to convert it into a numeric UID to submit reports.

1. From the main menu, select **[10] Get UID from Profile URL**.
2. Select an active account to perform the lookup.
3. Paste the profile URL.
4. The tool will fetch and display the exact numeric `UID` (e.g., `4`).

### Submitting Reports

1. Start the tool (`node cli.js`).
2. Select your target type: **[3] Report a Profile** or **[4] Report a Group**.
3. It will ask you which account(s) to report from. You can choose a specific account, or type **A** to use **ALL accounts** simultaneously.
4. Enter the **target UID** (or GID for groups).
5. Enter the **number of rounds** (default is 1).
6. Select your **Report Type**. You can choose:
   - `0` for a Random type each round
   - `1` to run All available types (22 for profile, 16 for group)
   - Or pick a specific category (e.g., Harassment, Fake Account, Terrorism).
7. The tool will submit the reports to Facebook and show a success/failure summary.

## Advanced CLI Mode (Automation)

For automated usage without the interactive menu, you can pass arguments directly:

```bash
# Report a profile (1x random type using all logged-in accounts)
node cli.js <UID>

# Report 5 rounds with random types
node cli.js <UID> --count 5

# Report with all 22 types, 1 round
node cli.js <UID> --type all

# Specific type
node cli.js <UID> --type fake_account

# Infinite mode (runs forever until you press Ctrl+C)
node cli.js <UID> --infinite

# Report a group
node cli.js group <GID> --type all --count 5

# List all available report types
node cli.js --types

# Help menu
node cli.js --help
```

## Available Report Types

### Profile (22 types)
`fake_account`, `harassment_me`, `harassment_someone`, `violence`, `violence_death`, `hate_speech`, `nudity`, `nudity_threats`, `impersonation`, `pretending_me`, `pretending_friend`, `pretending_someone`, `pretending_business`, `terrorism`, `scam`, `spam`, `suicide`, `child_nudity_threats`, `child_bullying`, `restricted_items`, `drugs`, `intellectual_property`

### Group (16 types)
`grp_bullying`, `grp_sexual_exploitation`, `grp_violence_death`, `grp_credible_threat`, `grp_trafficking`, `grp_terrorism`, `grp_violence`, `grp_hate_speech`, `grp_child_abuse`, `grp_animal_abuse`, `grp_weapons`, `grp_animals`, `grp_scam`, `grp_spam`, `grp_nudity`, `grp_suicide`
