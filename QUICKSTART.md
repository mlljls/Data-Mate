# 🚀 Data Studio AI — أوامر البدء السريع

## 1️⃣ التثبيت الأول

```bash
# استنساخ المشروع
git clone <repo-url> data-studio-ai
cd data-studio-ai

# تثبيت الحزم
npm install
```

---

## 2️⃣ تشغيل التطوير

### ويب (PWA):
```bash
npm run dev
# افتح http://localhost:5173
```

### Desktop (Electron):
```bash
# في نافذة أولى:
npm run dev

# في نافذة ثانية:
npm run dev:electron
```

### موبايل (Capacitor):
```bash
npm run dev
# في نافذة ثانية:
npx cap sync
npx cap open android  # أو npx cap open ios
```

---

## 3️⃣ البناء والنشر

### PWA — النشر على الويب:
```bash
npm run build
# انسخ مجلد `dist/` إلى:
# - Vercel.com
# - Netlify.com
# - Any web hosting
```

**رابط مثال بعد النشر:**
```
https://yourdomain.com
```

**التثبيت على الموبايل:**
1. افتح الرابط على المتصفح
2. اضغط على ☰ (menu) → "Install app"
3. سيتنزل على الشاشة الرئيسية

---

### Electron — Desktop App:
```bash
# بناء الملفات
npm run build:electron

# النتائج في:
# Windows: dist/Data Studio AI-1.0.0-x64.exe
# Mac: dist/Data Studio AI-1.0.0.dmg
# Linux: dist/data-studio-ai-1.0.0.AppImage
```

**توزيع التطبيق:**
- أرسل الملف `.exe` (Windows) مباشرة
- أرسل الملف `.dmg` (Mac) مباشرة
- أرسل `.AppImage` (Linux) مباشرة

---

### Capacitor — Android:
```bash
npm run build
npx cap add android
npx cap sync
npx cap open android

# في Android Studio:
# اختر Device/Emulator → اضغط ▶️ (Run)
```

**البناء النهائي (للـ Play Store):**
```bash
# Build → Generate Signed Bundle / APK
# اختر Release
# وقع بـ keystore الخاص بك
```

---

### Capacitor — iOS:
```bash
npm run build
npx cap add ios
npx cap sync
npx cap open ios

# في Xcode:
# اختر Team → اختر Device → اضغط ▶️
```

**البناء النهائي (للـ App Store):**
```bash
# Product → Archive
# Upload to App Store
```

---

## 4️⃣ أوامر مفيدة

### تطوير و معاينة:
```bash
npm run dev          # تطوير الويب مع hot reload
npm run preview      # معاينة الإصدار النهائي محلياً
```

### بناء الإصدارات:
```bash
npm run build              # بناء PWA
npm run build:electron     # بناء Electron
npm run build:apk          # بناء APK (Android)
npm run build:ios          # بناء IPA (iOS)
```

### المزامنة والتحديث:
```bash
npx cap sync       # تحديث الملفات على الأجهزة
npx cap update     # تحديث Capacitor نفسه
```

---

## 5️⃣ المتطلبات حسب المنصة

| المنصة | المتطلبات | الأمر |
|--------|-----------|-------|
| **PWA** | متصفح حديث | `npm run build` |
| **Electron** | Node.js فقط | `npm run build:electron` |
| **Android** | Android Studio + JDK 11+ | `npx cap open android` |
| **iOS** | Mac + Xcode | `npx cap open ios` |

---

## 6️⃣ مشاكل شائعة

### ❌ Port 5173 مشغول:
```bash
# غيّر المنفذ في vite.config.js أو:
npm run dev -- --port 5174
```

### ❌ Capacitor sync فشل:
```bash
npm run build      # تأكد أن dist موجود
rm -rf android ios # احذف القديم
npx cap add android && npx cap add ios
npx cap sync
```

### ❌ Electron لا يبدأ:
```bash
# تأكد أن dist موجود:
npm run build

# ثم جرب:
npm run dev:electron
```

---

## 7️⃣ الخطوات التالية

1. ✅ **اختبر محلياً**: `npm run dev`
2. ✅ **بناء PWA**: `npm run build` → انسخ لـ Vercel
3. ✅ **بناء Desktop**: `npm run build:electron` → وزع `.exe`/.dmg
4. ✅ **بناء موبايل**: `npx cap sync` → فتح في Studio

---

## 📞 للمساعدة:

- اقرأ `SETUP_GUIDE.md` للمزيد من التفاصيل
- تحقق من الـ `package.json` للسكريبتات المتاحة
- استخدم `npm run` لعرض جميع الأوامر

**عش تطويرك! 🚀**
