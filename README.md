# 🚀 LinkHub — دليل الإعداد الكامل

منصة خدمات ذكية جاهزة للنشر باستخدام Firebase + واتساب.

<div align="center">
  <br>
  <a href="https://ko-fi.com/coden1">
    <img src="https://storage.ko-fi.com/cdn/brandasset/kofi_button_orange.png" alt="Buy Me a Coffee" width="300" style="border-radius: 12px;" />
  </a>
  <p><i>دعمك يساعدنا على تطوير حلول برمجية مفتوحة المصدر ومبتكرة في <b>CODEN</b></i></p>
  <br>
</div>

---

## 📂 هيكل الملفات

```
linkhub/
├── index.html      ← واجهة العميل
├── admin.html      ← لوحة تحكم الأدمن
├── firebase.js     ← إعداد Firebase (عدّل بياناتك)
├── manifest.json   ← PWA manifest
└── README.md
```

---

## ⚙️ خطوات الإعداد

### 1. أنشئ مشروع Firebase
- اذهب إلى https://console.firebase.google.com
- أنشئ مشروع جديد
- فعّل: **Firestore** + **Realtime Database** + **Storage** + **Authentication**

### 2. احصل على بيانات الإعداد
- من Firebase Console → Project Settings → Web App
- انسخ `firebaseConfig`
- ضعها في `firebase.js`

### 3. غيّر رقم واتساب
في `index.html` — ابحث عن:
```js
const WHATSAPP_NUMBER = "966500000000";
```
غيّره لرقمك (بدون + أو مسافات).

### 4. غيّر بيانات الأدمن
في `admin.html` — ابحث عن:
```js
const ADMIN_USER = "admin";
const ADMIN_PASS = "admin123";
```
غيّرهم لبيانات آمنة.

---

## 🛒 إضافة منتجات حقيقية

في `index.html` — ابحث عن `const products = [...]`
وأضف منتجاتك بنفس الشكل:

```js
{ 
  id: 9, 
  name: "اسم الخدمة", 
  desc: "وصف مختصر", 
  price: 100,        // السعر الحالي
  old: 150,          // السعر القديم (null لو مافيش)
  icon: "🎯",        // emoji
  cat: "design",     // design | shipping | consulting | booking
  badge: "جديد"      // null | "جديد" | "شائع" | "sale"
}
```

---

## 🎟 كوبونات الخصم

في `index.html` ابحث عن:
```js
const COUPONS = { "SAVE20": 20, "LINK50": 50, "VIP30": 30 };
```
أضف كوباناتك: `"CODENAME": قيمة_الخصم_بالريال`

---

## 🌐 النشر (مجاناً)

### خيار 1 — Firebase Hosting
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy
```

### خيار 2 — Netlify
- اسحب المجلد مباشرة على https://netlify.com
- يعطيك رابط فوراً!

### خيار 3 — Vercel
```bash
npm install -g vercel
vercel --prod
```

---

## 🔐 تأمين لوحة الأدمن (للإنتاج)

استبدل نظام المرور البسيط بـ Firebase Auth:

```js
import { signInWithEmailAndPassword } from "firebase/auth";

async function doLogin() {
  const email = document.getElementById("loginUser").value;
  const pass  = document.getElementById("loginPass").value;
  try {
    await signInWithEmailAndPassword(auth, email, pass);
    // دخول ناجح
  } catch(e) {
    // خطأ
  }
}
```

---

## 📲 ربط Firebase Firestore للطلبات

```js
import { collection, addDoc, getDocs } from "firebase/firestore";

// حفظ طلب جديد
async function saveOrder(orderData) {
  await addDoc(collection(db, "orders"), {
    ...orderData,
    createdAt: new Date()
  });
}

// جلب الطلبات
async function loadOrders() {
  const snap = await getDocs(collection(db, "orders"));
  return snap.docs.map(d => ({ id: d.id, ...d.data() }));
}
```

---

## ⚡ مميزات المشروع

| الميزة | الوضع |
|--------|-------|
| واجهة عميل احترافية | ✅ جاهز |
| سلة طلبات ذكية | ✅ جاهز |
| إرسال واتساب تلقائي | ✅ جاهز |
| كوبونات خصم | ✅ جاهز |
| تتبع الطلبات | ✅ جاهز |
| شات دعم مباشر | ✅ جاهز |
| Flash Sale Timer | ✅ جاهز |
| عداد إحصائيات | ✅ جاهز |
| لوحة أدمن كاملة | ✅ جاهز |
| إدارة منتجات | ✅ جاهز |
| إدارة رسائل | ✅ جاهز |
| إدارة إعلانات | ✅ جاهز |
| إدارة تقييمات | ✅ جاهز |
| PWA manifest | ✅ جاهز |
| Firebase Firestore | 🔧 يحتاج ربط |
| Firebase Auth | 🔧 يحتاج ربط |
| إشعارات واتساب تلقائية | 🔧 يحتاج Twilio/360dialog |

---

## 📞 الدعم

أي استفسار؟ راسلنا على واتساب مباشرة!
