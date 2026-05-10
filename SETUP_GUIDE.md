# Data Studio AI — دليل التطوير والنشر

تطبيق شامل لتحليل وتنظيف البيانات يعمل على كل الأجهزة.

---

## 🚀 البدء السريع

### 1️⃣ التثبيت الأساسي

```bash
# استنساخ المشروع
git clone <repo-url>
cd data-studio-ai

# تثبيت الحزم
npm install

# تشغيل التطوير
npm run dev
```

ثم افتح `http://localhost:5173` في المتصفح.

---

## 📱 PWA (Progressive Web App) — موبايل + ويب

### تثبيت التطبيق على أي جهاز:

1. **على المتصفح**: 
   - افتح `https://yourdomain.com`
   - اضغط على زر التثبيت (أو الثلاث نقاط → Install app)
   - سيتنزل على الشاشة الرئيسية

2. **الميزات**:
   - ✅ يعمل بدون انترنت (offline)
   - ✅ تحديث تلقائي
   - ✅ مثل التطبيق الأصلي

### النشر:

```bash
# بناء الإصدار الإنتاجي
npm run build

# ستجد الملفات في مجلد `dist/`
# انسخ المجلد كاملاً لـ hosting مثل:
# - Vercel
# - Netlify
# - GitHub Pages
```

---

## 🖥️ Electron (Windows / Mac / Linux)

### لتطوير تطبيق Desktop:

```bash
# شغّل التطبيق أثناء التطوير
npm run dev:electron

# أو في نافذة منفصلة:
# في النافذة الأولى:
npm run dev

# في نافذة ثانية:
npm start:electron
```

### بناء التطبيق للنشر:

```bash
# على Windows
npm run build:electron
# سينتج: `dist/Data Studio AI-version-x64.exe` و `.zip`

# على Mac
npm run build:electron
# سينتج: `dist/Data Studio AI-version.dmg`

# على Linux
npm run build:electron
# سينتج: `dist/data-studio-ai-version.AppImage` و `.deb`
```

**توزيع التطبيق**:
- Windows: أرسل ملف `.exe` أو `.zip`
- Mac: أرسل ملف `.dmg`
- Linux: أرسل `.AppImage` أو `.deb`

---

## 📲 Capacitor (Android / iOS)

### إعداد Android:

```bash
# تثبيت Capacitor
npm install --save-dev @capacitor/cli @capacitor/android @capacitor/ios

# البناء الأول
npm run build
npx cap add android
npx cap sync

# فتح Android Studio
npx cap open android

# اختر الجهاز/المحاكي ثم اضغط Run
```

### إعداد iOS:

```bash
# البناء الأول
npm run build
npx cap add ios
npx cap sync

# فتح Xcode
npx cap open ios

# اختر الجهاز ثم اضغط Build + Run
```

### التطوير المباشر:

```bash
# تحديث التطبيق أثناء التطوير
npm run dev      # في نافذة أولى
npx cap sync     # في نافذة ثانية (كل مرة تعدل)
```

---

## 🌐 الإعدادات حسب الجهاز

### iOS (App Store)

1. أنشئ حساب Apple Developer ($99/سنة)
2. أنشئ App ID و Provisioning Profile
3. فتح المشروع في Xcode
4. Signing & Capabilities → اختر Team
5. Product → Archive → Upload

### Android (Google Play)

1. أنشئ حساب Google Play ($25 مرة واحدة)
2. أنشئ keystore (مهم جداً):

```bash
keytool -genkey -v -keystore my-key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias my-key-alias
```

3. فتح `android/app/build.gradle`:

```gradle
signingConfigs {
    release {
        keyAlias 'my-key-alias'
        keyPassword 'YOUR_PASSWORD'
        storeFile file('../../my-key.jks')
        storePassword 'YOUR_PASSWORD'
    }
}
```

4. Build → Build Bundle(s) / APK(s)

---

## 📊 ملخص الخيارات

| الخيار | الأجهزة | البدء | النشر | الصعوبة |
|---------|---------|-------|-------|---------|
| **PWA** | ويب + كل الأجهزة | `npm run dev` + رابط | Vercel/Netlify | سهل جداً |
| **Electron** | Windows/Mac/Linux | `npm run dev:electron` | `.exe`/`.dmg` | متوسط |
| **Capacitor** | Android/iOS | `npm run build && npx cap sync` | Play Store/App Store | متوسط |

---

## 🔧 توصيات للإنتاج

### 1. PWA (للبدء السريع):
```bash
npm run build
# انسخ المجلد dist/ لـ Vercel
```

### 2. Desktop (Windows/Mac):
```bash
npm run build:electron
# سيتم إنشاء ملفات قابلة للتنزيل
```

### 3. موبايل (الخطوة النهائية):
- استخدم Capacitor بعد استقرار التطبيق
- ركز على Android أولاً (أسهل)
- iOS يتطلب Mac

---

## 🐛 حل المشاكل

### PWA لا يعمل بدون إنترنت
✅ تحقق أن `vite-plugin-pwa` مثبت
✅ تأكد من `manifest.json` صحيح
✅ امسح Service Worker القديم: `Clear Site Data`

### Electron لا يبدأ
✅ تحقق أن النافذة على `localhost:5173`
✅ استخدم `npm run dev:electron` (تشغيل متزامن)
✅ تأكد من وجود ملف `electron.js` في الجذر

### Capacitor build فشل
✅ استخدم `npx cap sync` قبل البناء
✅ تحقق أن `dist/` موجود: `npm run build` أولاً
✅ على Android: تحقق من تثبيت Java JDK 11+

---

## 📝 الملفات الأساسية

```
data-studio-ai/
├── src/
│   ├── App.jsx          # كود React الرئيسي
│   ├── App.css          # الأنماط
│   ├── main.jsx         # نقطة البداية
│   └── index.html       # صفحة HTML
├── electron.js          # كود Electron (Desktop)
├── vite.config.js       # إعدادات Vite + PWA
├── package.json         # الحزم والسكريبتات
├── capacitor.config.json # إعدادات Capacitor (Mobile)
└── public/
    ├── manifest.json    # PWA manifest
    ├── sw.js           # Service Worker
    └── icons/          # أيقونات التطبيق
```

---

## ✨ الخطوات التالية

1. **اختبر على أجهزة فعلية**:
   - موبايل: استخدم `ngrok` لـ local testing
   - Desktop: اختبر على Windows/Mac/Linux

2. **أضف ميزات**:
   - تحسين Offline Mode
   - Local Storage للبيانات
   - Web Workers للعمليات الثقيلة

3. **نشر الإصدار الأول**:
   - PWA على Vercel/Netlify
   - Electron على GitHub Releases
   - Capacitor على Play Store (تحديثات مستقبلية)

---

## 📚 موارد إضافية

- [Vite Documentation](https://vitejs.dev)
- [Electron Documentation](https://www.electronjs.org/docs)
- [Capacitor Documentation](https://capacitorjs.com/docs)
- [PWA Documentation](https://web.dev/progressive-web-apps/)

---

**أي استفسار؟ اسأل Claude AI والمشروع سيساعدك! 🤖**
