# Life Level Up

বাংলা UI-সহ offline-first Cordova Android prototype.

## ফিচার
- Daily/weekly Quest যোগ করা
- Easy / Medium / Hard difficulty অনুযায়ী XP ও Coins
- XP থেকে Level গণনা ও Level Up notification
- Daily completion streak
- Reward Shop ও নিজস্ব reward
- Dark/Light theme
- JSON Backup / Restore
- লোকাল তারিখ `YYYY-MM-DD` হিসাবে ডিভাইসের timezone ব্যবহার করে

## GitHub থেকে APK বানানো
1. এই ZIP extract করে সব ফাইল GitHub repository-র root-এ upload করো; `.github/workflows/build-apk.yml`-সহ hidden folder-টিও upload করতে হবে।
2. Repository-তে `Actions` tab খোলো।
3. `Build Android APK` workflow নির্বাচন করে `Run workflow` চাপো, অথবা `main` branch-এ push হওয়া পর্যন্ত অপেক্ষা করো।
4. Workflow শেষ হলে run-এর নিচে `Artifacts` থেকে `life-level-up-debug-apk` download করো।
5. ZIP extract করে `app-debug.apk` ফোনে ইনস্টল করো। Android চাইলে browser/file manager-এর জন্য install permission দাও।

## গুরুত্বপূর্ণ: signing key
এই initial workflow একটি **debug-signed APK** বানায়, যাতে প্রথমবার সহজে পরীক্ষা করা যায়। GitHub-hosted runner-এর debug signing key স্থায়ী নয়; তাই পরের build-এর APK-তে update install নাও হতে পারে। ডেটা মুছে না ফেলার নিশ্চয়তার জন্য production/update release-এর আগে নিজের স্থায়ী keystore তৈরি করে GitHub Actions Secrets-এ `SIGNING_KEYSTORE_BASE64`, `SIGNING_STORE_PASSWORD`, `SIGNING_KEY_ALIAS`, `SIGNING_KEY_PASSWORD` হিসেবে সেট করে release-signing workflow যোগ করতে হবে। Keystore নিরাপদে আলাদা করে রাখবে এবং কখনো public repository-তে commit করবে না। একই package ID (`com.liferpg.lifelevelup`) অপরিবর্তিত রাখতে হবে।

## ডেটা ও ব্যাকআপ
ডেটা WebView-এর localStorage-এ থাকে। অ্যাপ uninstall করলে বা Android app data clear করলে ডেটা মুছে যেতে পারে। Restore বর্তমান ডেটা প্রতিস্থাপন করে—Restore করার আগে বর্তমান Backup নাও। প্রথম APK-তে কোনো cloud sync নেই।

## সীমাবদ্ধতা
- এটি initial prototype, production release নয়।
- JSON export Android WebView-এ ডাউনলোড আচরণ ডিভাইসভেদে ভিন্ন হতে পারে; সমস্যা হলে browser-এ পরীক্ষা বা native file picker integration দরকার হতে পারে।
- `Playwright` CI-তে আলাদা করে configure করা হয়নি; প্রাথমিক static checks ও JavaScript parse validation আলাদাভাবে চালাতে হবে।
