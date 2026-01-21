# ⚽ Halı Saha Randevu Sistemi

Halı saha rezervasyonu ve yönetimi için geliştirilmiş full-stack mobil uygulama. Flutter ile geliştirilen mobil uygulama ve Node.js/Express backend API'si ile kullanıcıların halı saha randevuları oluşturmasını, ilan vermesini ve kadro kurmasını sağlar.

## 🚀 Özellikler

### 🎯 Temel Özellikler
- **Kullanıcı Yönetimi**: Firebase Authentication ile güvenli kayıt ve giriş
- **Randevu Sistemi**: Halı saha rezervasyonu oluşturma ve yönetme
- **İlan Sistemi**: Maç ilanları oluşturma ve katılım
- **Kadro Oluşturma**: Takım kadroları kurma ve yönetme
- **Anlık Mesajlaşma**: Kullanıcılar arası sohbet özelliği
- **Duyuru Sistemi**: Önemli duyuruların paylaşılması
- **Profil Yönetimi**: Kullanıcı profili düzenleme ve fotoğraf yükleme
- **Geri Bildirim**: Kullanıcı önerileri ve şikayetleri için feedback sistemi

### 🛡️ Güvenlik
- Firebase Admin SDK ile güvenli kimlik doğrulama
- JWT token bazlı oturum yönetimi
- Bcrypt ile şifreli password hashleme
- Environment variables ile hassas bilgilerin korunması

## 🏗️ Teknoloji Stack

### Backend
- **Node.js** & **Express.js** - REST API
- **PostgreSQL** - İlişkisel veritabanı
- **Firebase Admin SDK** - Kimlik doğrulama
- **Multer** - Dosya yükleme
- **Nodemailer** - E-posta gönderimi
- **JWT** - Token bazlı yetkilendirme

### Frontend (Mobile)
- **Flutter** - Cross-platform mobil uygulama
- **Dart** - Programlama dili
- **Provider** - State management
- **Firebase** - Authentication ve Cloud Messaging
- **HTTP** - API iletişimi

### Veritabanı
- **PostgreSQL** - Ana veritabanı
- **Supabase** - Veritabanı hosting (opsiyonel)

## 📋 Gereksinimler

### Backend
- Node.js (v14 veya üzeri)
- PostgreSQL (v12 veya üzeri)
- npm veya yarn paket yöneticisi

### Mobile
- Flutter SDK (v3.8.1 veya üzeri)
- Dart SDK
- Android Studio / Xcode (platform bazlı)

## 🔧 Kurulum

### Backend Kurulumu

1. **Repository'yi klonlayın:**
```bash
git clone https://github.com/Mustafaesat/Halisaha_Randevu.git
cd Halisaha_Randevu/backend
```

2. **Bağımlılıkları yükleyin:**
```bash
npm install
```

3. **PostgreSQL veritabanını oluşturun:**
```bash
# PostgreSQL'e bağlanın
psql -U postgres

# Veritabanını oluşturun
CREATE DATABASE halisaha_proje_db;

# Şemaları yükleyin
\i database/schema.sql
```

4. **Environment değişkenlerini ayarlayın:**

`.env.example` dosyasını `.env` olarak kopyalayın:
```bash
cp .env.example .env
```

`.env` dosyasını düzenleyin ve aşağıdaki bilgileri girin:

```env
# Database Configuration
DATABASE_URL=your_supabase_connection_string
# VEYA local PostgreSQL kullanıyorsanız:
DB_HOST=localhost
DB_USER=postgres
DB_PASSWORD=your_password
DB_NAME=halisaha_proje_db
DB_PORT=5432

# Server Configuration
PORT=3001

# Firebase Admin SDK Configuration
# Firebase Console > Project Settings > Service Accounts'tan alın
FIREBASE_PROJECT_ID=your-project-id
FIREBASE_PRIVATE_KEY_ID=your-private-key-id
FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\nYour-Private-Key-Here\n-----END PRIVATE KEY-----\n"
FIREBASE_CLIENT_EMAIL=your-service-account@your-project-id.iam.gserviceaccount.com
FIREBASE_CLIENT_ID=your-client-id
FIREBASE_CLIENT_CERT_URL=https://www.googleapis.com/robot/v1/metadata/x509/your-service-account%40your-project-id.iam.gserviceaccount.com

# Email Configuration (Opsiyonel)
EMAIL_USER=your-email@gmail.com
EMAIL_PASSWORD=your-app-password
```

**Firebase Credentials Nasıl Alınır?**
1. [Firebase Console](https://console.firebase.google.com/) → Projenizi seçin
2. Project Settings → Service Accounts
3. "Generate new private key" butonuna tıklayın
4. İndirilen JSON dosyasındaki değerleri `.env` dosyasına kopyalayın
5. `private_key` değerini kopyalarken `\n` karakterlerini koruyun

5. **Sunucuyu başlatın:**
```bash
# Development mode
npm run dev

# Production mode
npm start
```

Backend şimdi `http://localhost:3001` adresinde çalışıyor olmalı.

### Mobile Kurulumu

1. **Mobile dizinine gidin:**
```bash
cd ../mobile
```

2. **Flutter bağımlılıklarını yükleyin:**
```bash
flutter pub get
```

3. **Firebase yapılandırması:**

`lib/firebase_options.dart` dosyasında Firebase ayarlarınızı güncelleyin:
- [Firebase Console](https://console.firebase.google.com/) → Projeniz → Project Settings
- "Add app" butonuyla Android/iOS uygulamanızı ekleyin
- Yapılandırma dosyalarını indirip projeye ekleyin

4. **API endpoint'ini ayarlayın:**

`lib/services/api_service.dart` veya ilgili servis dosyalarında backend URL'ini güncelleyin:
```dart
static const String baseUrl = 'http://10.0.2.2:3001'; // Android emulator için
// veya
static const String baseUrl = 'http://localhost:3001'; // iOS simulator için
// veya
static const String baseUrl = 'https://your-backend-url.com'; // Production için
```

5. **Uygulamayı çalıştırın:**
```bash
# Android için
flutter run

# iOS için
flutter run

# Web için
flutter run -d chrome
```

## 📁 Proje Yapısı

```
Halisaha-Projesi/
├── backend/
│   ├── config/           # Veritabanı ve Firebase yapılandırması
│   ├── controllers/      # Route controller'ları
│   ├── database/         # SQL şemaları ve migration'lar
│   ├── middleware/       # Express middleware'leri
│   ├── routes/           # API route tanımları
│   ├── uploads/          # Yüklenen dosyalar
│   ├── utils/            # Yardımcı fonksiyonlar
│   ├── .env.example      # Environment değişkenleri örneği
│   ├── server.js         # Ana sunucu dosyası
│   └── package.json      # Backend bağımlılıkları
│
└── mobile/
    ├── lib/
    │   ├── models/       # Veri modelleri
    │   ├── providers/    # State management
    │   ├── screens/      # UI ekranları
    │   ├── services/     # API servisleri
    │   ├── widgets/      # Yeniden kullanılabilir widget'lar
    │   ├── firebase_options.dart
    │   └── main.dart     # Ana uygulama dosyası
    ├── assets/           # Görseller ve statik dosyalar
    ├── android/          # Android native kodu
    ├── ios/              # iOS native kodu
    └── pubspec.yaml      # Flutter bağımlılıkları
```

## 🗄️ Veritabanı Şeması

Proje aşağıdaki ana tablolardan oluşur:
- **kullanicilar** - Kullanıcı bilgileri
- **randevular** - Halı saha randevuları
- **ilanlar** - Maç ilanları
- **kadrolar** - Takım kadroları
- **sohbetler** - Sohbet odaları
- **mesajlar** - Chat mesajları
- **duyurular** - Sistem duyuruları
- **feedback** - Kullanıcı geri bildirimleri

Detaylı şema için `backend/database/schema.sql` dosyasına bakın.

## 🔌 API Endpoints

### Authentication
- `POST /auth/register` - Yeni kullanıcı kaydı
- `POST /auth/login` - Kullanıcı girişi
- `POST /auth/verify-token` - Token doğrulama
- `POST /auth/reset-password` - Şifre sıfırlama
- `POST /auth/confirm-reset-password` - Şifre sıfırlama onayı

### Randevular
- `GET /randevular` - Tüm randevuları listele
- `GET /randevular/:id` - Randevu detayı
- `POST /randevular` - Yeni randevu oluştur
- `PUT /randevular/:id` - Randevu güncelle
- `DELETE /randevular/:id` - Randevu sil

### İlanlar
- `GET /ilanlar` - Tüm ilanları listele
- `GET /ilanlar/:id` - İlan detayı
- `POST /ilanlar` - Yeni ilan oluştur
- `PUT /ilanlar/:id` - İlan güncelle
- `DELETE /ilanlar/:id` - İlan sil

### Profil
- `GET /profile/:userId` - Kullanıcı profili
- `PUT /profile/:userId` - Profil güncelle
- `PUT /profile/:userId/change-password` - Şifre değiştir
- `POST /profile/:userId/photo` - Profil fotoğrafı yükle

Tüm endpoint'ler için detaylı dokümantasyon: `backend/API_DOCS.md`

## 🧪 Test

### Backend Testleri
```bash
cd backend
npm test
```

### Mobile Testleri
```bash
cd mobile
flutter test
```

## 🚀 Deployment

### Backend Deployment
Backend'i Heroku, Render, Railway veya DigitalOcean'a deploy edebilirsiniz.

**Heroku Örneği:**
```bash
heroku create halisaha-backend
heroku addons:create heroku-postgresql:hobby-dev
heroku config:set FIREBASE_PROJECT_ID=your-project-id
heroku config:set FIREBASE_PRIVATE_KEY="your-private-key"
# Diğer environment variable'ları ekleyin
git push heroku main
```

### Mobile Deployment
**Android:**
```bash
flutter build apk --release
# veya
flutter build appbundle --release
```

**iOS:**
```bash
flutter build ios --release
```

## 🤝 Katkıda Bulunma

1. Bu repository'yi fork edin
2. Feature branch'i oluşturun (`git checkout -b feature/amazing-feature`)
3. Değişikliklerinizi commit edin (`git commit -m 'Add amazing feature'`)
4. Branch'inizi push edin (`git push origin feature/amazing-feature`)
5. Pull Request oluşturun

## 📝 Lisans

Bu proje [MIT lisansı](LICENSE) altında lisanslanmıştır.

## 👤 İletişim

Mustafa Esat - [GitHub](https://github.com/Mustafaesat)

Proje Link: [https://github.com/Mustafaesat/Halisaha_Randevu](https://github.com/Mustafaesat/Halisaha_Randevu)

## 🙏 Teşekkürler

- Flutter ekibine harika framework için
- Firebase ekibine kolay authentication için
- PostgreSQL topluluğuna güçlü veritabanı için

---

⭐ Bu projeyi beğendiyseniz yıldız vermeyi unutmayın!