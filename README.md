# Recyclable Trash Classification Android App 🌱♻️

[![Android](https://img.shields.io/badge/Platform-Android-green.svg)](https://developer.android.com)
[![Firebase](https://img.shields.io/badge/Backend-Firebase-orange.svg)](https://firebase.google.com)
[![TensorFlow Lite](https://img.shields.io/badge/ML-TensorFlow%20Lite-blue.svg)](https://www.tensorflow.org/lite)
[![Stripe](https://img.shields.io/badge/Payment-Stripe-purple.svg)](https://stripe.com)

## 📋 Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [System Architecture](#system-architecture)
- [Machine Learning Model](#machine-learning-model)
- [User Roles & Access Control](#user-roles--access-control)
- [Database Schema](#database-schema)
- [Installation & Setup](#installation--setup)
- [Usage Guide](#usage-guide)
- [API Integrations](#api-integrations)
- [Security Features](#security-features)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)

---

## 🌟 Overview

The **Recyclable Trash Classification App** is a comprehensive Android application that combines AI-powered waste classification with a complete business ecosystem for waste management. The app enables users to classify recyclable materials using machine learning while facilitating seamless communication and transactions between waste collectors and dealers.

### 🎯 Core Objectives
- **Intelligent Waste Classification**: AI-powered identification of recyclable materials
- **Business Platform**: Connect collectors and dealers in the recycling industry
- **Secure Transactions**: Integrated payment system for business operations
- **Real-time Communication**: Chat system for seamless coordination
- **Administrative Control**: Comprehensive admin panel for system management

---

## ✨ Features

### 🤖 AI-Powered Classification
- **13 Recyclable Categories**: Paper, Plastic, Glass, Metal, Electronics, Clothes, etc.
- **Real-time Image Processing**: Instant classification with 90% confidence threshold
- **Camera & Gallery Support**: Multiple image input methods
- **Image Editing**: Built-in cropping and editing capabilities
- **Classification History**: Track and review past classifications

### 💼 Business Platform
- **Multi-Role System**: Admin, Dealers, Collectors, Regular Users
- **Permit Applications**: Streamlined application process for dealers and collectors
- **Location Services**: GPS-enabled dealer location mapping
- **Profile Management**: Comprehensive user profiles with verification

### 💬 Communication System
- **Real-time Chat**: Instant messaging between dealers and collectors
- **Role-based Access**: Targeted communication channels
- **Message History**: Persistent chat records
- **User Discovery**: Find and connect with relevant users

### 💳 Payment Integration
- **Stripe Integration**: Secure payment processing
- **Transaction History**: Complete payment records
- **Multi-currency Support**: USD-based transactions
- **Payment Analytics**: Track financial activities

### 🛡️ Administrative Features
- **User Management**: Control user roles and permissions
- **Application Review**: Approve/reject permit applications
- **System Analytics**: Monitor app usage and statistics
- **Content Moderation**: Oversee platform activities

---

## 🛠 Technology Stack

### **Frontend**
- **Language**: Java
- **UI Framework**: Android Native with Material Design
- **Image Processing**: Glide for image loading and caching
- **Image Editing**: UCrop library for image cropping
- **Animations**: Lottie for smooth animations

### **Backend Services**
- **Authentication**: Firebase Authentication
- **Database**: Firebase Realtime Database
- **Storage**: Firebase Cloud Storage
- **Cloud Services**: Firebase Cloud Firestore

### **Machine Learning**
- **Framework**: TensorFlow Lite
- **Model Source**: Google Teachable Machine
- **Input Format**: 224x224x3 RGB images
- **Output**: 14-class classification with confidence scores

### **External APIs**
- **Payment**: Stripe API v22.2.0
- **Maps**: Google Maps API
- **Networking**: Volley for HTTP requests

### **Development Tools**
- **Build System**: Gradle with Kotlin DSL
- **Min SDK**: API 24 (Android 7.0)
- **Target SDK**: API 33 (Android 13)
- **Compile SDK**: API 34

---

## 🏗 System Architecture

```
┌─────────────────────────────────────────────────────┐
│                 PRESENTATION LAYER                  │
├─────────────────────────────────────────────────────┤
│  Activities  │  Fragments  │  Adapters  │  Views    │
├─────────────────────────────────────────────────────┤
│                 BUSINESS LOGIC LAYER                │
├─────────────────────────────────────────────────────┤
│  User Mgmt   │  ML Service │  Chat Mgmt │  Payment  │
├─────────────────────────────────────────────────────┤
│                    DATA LAYER                       │
├─────────────────────────────────────────────────────┤
│  Firebase    │  Local       │  SharedPrefs │  Cache  │
│  Database    │  Storage     │             │         │
├─────────────────────────────────────────────────────┤
│                 EXTERNAL SERVICES                   │
├─────────────────────────────────────────────────────┤
│  Firebase    │  Stripe API  │  Google     │  ML      │
│  Services    │             │  Maps       │  Model   │
└─────────────────────────────────────────────────────┘
```

### **Data Flow Architecture**
```
User Input → ML Classification → Firebase Storage → 
UI Update → History Save → Real-time Sync
```

---

## 🧠 Machine Learning Model

### **Model Specifications**
```yaml
Model Type: Image Classification
Framework: TensorFlow Lite
Input Shape: [1, 224, 224, 3]
Output Shape: [1, 14]
Data Type: FLOAT32
Model Size: ~4MB (optimized for mobile)
```

### **Classification Categories**
| Category | Sub-types | Recyclable |
|----------|-----------|------------|
| **Glass** | Bottles, Jars | ✅ |
| **Plastic** | Bottles, Containers, Jugs, Mugs, Buckets | ✅ |
| **Paper** | Newspaper, Regular Paper, Shopping Bags, Cardboard | ✅ |
| **Metal** | Cans | ✅ |
| **Textiles** | Clothes | ✅ |
| **Non-Recyclable** | Mixed/Unknown materials | ❌ |

### **Classification Logic**
```java
// Confidence threshold: 90%
if (confidence > 0.9) {
    if (classIndex < 13) {
        result = "Recyclable";
    } else {
        result = "Non Recyclable";
    }
} else {
    result = "Non Recyclable"; // Low confidence
}
```

### **Model Performance**
- **Accuracy**: 90%+ confidence threshold
- **Inference Time**: <500ms on mid-range devices
- **Memory Usage**: ~50MB during inference
- **Supported Formats**: JPEG, PNG

---

## 👥 User Roles & Access Control

### **1. Admin User** 🔑
```yaml
Identifier: admin@gmail.com
Profile Code: "admin"
Permissions:
  - Full system access
  - User management
  - Application approval/rejection
  - System analytics
  - Content moderation
Features:
  - Admin Panel
  - User statistics
  - Application management
  - Profile oversight
```

### **2. Dealer** 🏢
```yaml
Profile Code: "5"
Permissions:
  - Make payments to collectors
  - Chat with collectors
  - View collector locations
  - Apply for dealer permits
Features:
  - Payment initiation
  - Map view of collectors
  - Chat system
  - Transaction history
  - Permit application
```

### **3. Collector** 👷
```yaml
Profile Code: "2"
Permissions:
  - Receive payments from dealers
  - Chat with dealers
  - Apply for collection permits
Features:
  - Payment reception
  - Chat system
  - Transaction history
  - Permit application
  - Profile management
```

### **4. Regular User** 👤
```yaml
Profile Code: "1"
Permissions:
  - Image classification
  - View classification history
  - Profile management
Features:
  - AI classification
  - History tracking
  - Basic profile settings
```

---

## 🗄 Database Schema

### **Firebase Realtime Database Structure**

```json
{
  "user": {
    "userId": {
      "userId": "string",
      "userName": "string",
      "userEmail": "string",
      "userProfile": "1|2|5|admin"
    }
  },
  
  "Profiles": {
    "profileId": {
      "id": "string",
      "name": "string",
      "birthdate": "string",
      "uid": "string",
      "phone": "string",
      "email": "string",
      "nid": "string",
      "experiences": "string",
      "photoUrl": "string",
      "lat": "string",
      "lan": "string"
    }
  },
  
  "DealerProfiles": {
    "dealerId": {
      "id": "string",
      "name": "string",
      "birthdate": "string",
      "uid": "string",
      "phone": "string",
      "email": "string",
      "lat": "string",
      "lan": "string",
      "nid": "string",
      "experiences": "string",
      "photoUrl": "string"
    }
  },
  
  "history": {
    "userId": {
      "historyId": {
        "time": "dd/MM/yyyy HH:mm:ss",
        "imageUrl": "string",
        "name": "string",
        "historyId": "string"
      }
    }
  },
  
  "Chats": {
    "chatId": {
      "messageId": {
        "senderId": "string",
        "receiverId": "string",
        "message": "string",
        "timestamp": "long"
      }
    }
  },
  
  "Payments": {
    "chatId": {
      "paymentId": {
        "paymentId": "string",
        "senderId": "string",
        "receiverId": "string",
        "amount": "long",
        "timestamp": "long"
      }
    }
  },
  
  "ApplicationForms": {
    "applicationId": {
      "id": "string",
      "name": "string",
      "birthdate": "string",
      "phone": "string",
      "street": "string",
      "ward": "string",
      "city": "string",
      "zip": "string",
      "nid": "string",
      "experiences": "string",
      "photoUrl": "string",
      "status": "pending|approved|rejected"
    }
  }
}
```

### **Firebase Storage Structure**
```
gs://recyclabletrash-49901.firebasestorage.app/
├── history/
│   └── {userId}/
│       └── {timestamp}.jpg
├── profiles/
│   └── {userId}/
│       └── profile.jpg
└── applications/
    └── {applicationId}/
        └── documents/
```

---

## 🚀 Installation & Setup

### **Prerequisites**
- Android Studio Arctic Fox or later
- JDK 8 or higher
- Android SDK API 24+
- Firebase project setup
- Google Maps API key
- Stripe account (for payments)

### **1. Clone Repository**
```bash
git clone https://github.com/BasakArghy/RecyclableTrashClassification.git
cd RecyclableTrashClassification
```

### **2. Firebase Configuration**
1. Create a Firebase project at [Firebase Console](https://console.firebase.google.com)
2. Add Android app with package name: `com.example.recyclabletrashclassificationapp`
3. Download `google-services.json` and place in `app/` directory
4. Enable Authentication, Realtime Database, and Storage

### **3. API Keys Setup**
Create `local.properties` file in project root:
```properties
# Google Maps API Key
MAPS_API_KEY=your_google_maps_api_key

# Stripe Keys (Test Environment)
STRIPE_PUBLISHABLE_KEY=pk_test_your_publishable_key
STRIPE_SECRET_KEY=sk_test_your_secret_key
```

### **4. Firebase Database Rules**
```json
{
  "rules": {
    "user": {
      "$uid": {
        ".read": "$uid === auth.uid",
        ".write": "$uid === auth.uid"
      }
    },
    "Chats": {
      "$chatId": {
        ".read": "auth != null",
        ".write": "auth != null"
      }
    },
    "Payments": {
      "$chatId": {
        ".read": "auth != null",
        ".write": "auth != null"
      }
    }
  }
}
```

### **5. Build and Run**
```bash
./gradlew assembleDebug
./gradlew installDebug
```

---

## 📱 Usage Guide

### **For Regular Users**
1. **Registration**: Create account with email/password
2. **Classification**: 
   - Tap camera button to capture image
   - Or select from gallery
   - View classification results
   - Check confidence scores
3. **History**: Review past classifications
4. **Profile**: Manage personal information

### **For Collectors**
1. **Application**: Apply for collector permit
2. **Approval**: Wait for admin approval
3. **Profile Setup**: Complete profile information
4. **Communication**: Chat with dealers
5. **Payments**: Receive payments for services

### **For Dealers**
1. **Application**: Apply for dealer permit
2. **Verification**: Submit required documents
3. **Profile**: Set up business profile with location
4. **Discovery**: Find collectors via map
5. **Transactions**: Make payments for collected materials

### **For Administrators**
1. **Dashboard**: Monitor system statistics
2. **Applications**: Review and approve permits
3. **User Management**: Oversee user activities
4. **Analytics**: Track app performance

---

## 🔌 API Integrations

### **Firebase Services**
```yaml
Authentication:
  Methods: [Email/Password, Password Reset]
  Security: Firebase Auth tokens

Database:
  Type: Realtime Database
  Sync: Real-time data synchronization
  Security: Custom security rules

Storage:
  Purpose: Image and document storage
  Compression: Automatic image optimization
  CDN: Global content delivery
```

### **Stripe Payment API**
```yaml
Version: v22.2.0
Environment: Test Mode
Features:
  - Payment Intents
  - Customer Management
  - Ephemeral Keys
  - Payment Methods
Currency: USD
Security: PCI DSS Compliant
```

### **Google Maps API**
```yaml
Services:
  - Maps SDK for Android
  - Places API
  - Geocoding API
Features:
  - Location display
  - Marker management
  - User location
Permissions: ACCESS_FINE_LOCATION
```

---

## 🔐 Security Features

### **Authentication Security**
- Firebase Authentication with secure tokens
- Password strength validation (minimum 6 characters)
- Email verification for account activation
- Session management with auto-logout

### **Data Protection**
- Encrypted data transmission (HTTPS/WSS)
- Firebase Security Rules for data access control
- User data isolation by UID
- Secure image upload with validation

### **Payment Security**
- PCI DSS compliant Stripe integration
- Tokenized payment processing
- Secure API key management
- Transaction encryption

### **Privacy Controls**
- Role-based access control (RBAC)
- Data minimization principles
- User consent for location services
- Secure storage of sensitive information

---

## 📁 Project Structure

```
RecyclableTrashClassification/
├── app/
│   ├── build.gradle.kts              # App-level build configuration
│   ├── google-services.json          # Firebase configuration
│   ├── model.tflite                  # TensorFlow Lite model
│   └── src/
│       ├── main/
│       │   ├── AndroidManifest.xml   # App permissions and activities
│       │   ├── java/com/example/recyclabletrashclassificationapp/
│       │   │   ├── MainActivity.java              # Main classification screen
│       │   │   ├── LoginScreen.java               # Authentication
│       │   │   ├── ChatActivity.java              # Chat list
│       │   │   ├── MessageActivity.java           # Individual chat
│       │   │   ├── AdminPanel.java                # Admin dashboard
│       │   │   ├── PaymentTransaction.java        # Payment model
│       │   │   ├── UserModel.java                 # User data model
│       │   │   ├── MapView.java                   # Location services
│       │   │   └── [Other Activities and Models]
│       │   ├── res/
│       │   │   ├── layout/            # UI layouts
│       │   │   ├── drawable/          # Images and icons
│       │   │   ├── values/            # Strings, colors, styles
│       │   │   └── menu/              # Navigation menus
│       │   └── ml/
│       │       └── model.tflite       # ML model file
│       └── test/                      # Unit tests
├── gradle/                            # Gradle wrapper
├── build.gradle.kts                   # Project-level build config
├── settings.gradle.kts                # Project settings
└── README.md                          # This documentation
```

### **Key Components**

#### **Core Activities**
- `MainActivity.java` - Image classification and main navigation
- `LoginScreen.java` - User authentication and registration
- `ChatActivity.java` - Chat system for dealers and collectors
- `MessageActivity.java` - Individual conversations with payment integration
- `AdminPanel.java` - Administrative controls and analytics

#### **Data Models**
- `UserModel.java` - User profile and role management
- `PaymentTransaction.java` - Payment transaction records
- `ChatMessage.java` - Chat message structure
- `HistoryModel.java` - Classification history
- `DealerProfileModel.java` - Dealer business profiles

#### **Adapters & UI**
- `MessageAdapter.java` - Chat message display
- `TransactionAdapter.java` - Payment history display
- `HistoryAdapter.java` - Classification history
- Various profile and application adapters

---

## 🤝 Contributing

### **Development Guidelines**
1. **Code Style**: Follow Android Code Style Guidelines
2. **Testing**: Write unit tests for business logic
3. **Documentation**: Comment complex algorithms and business logic
4. **Security**: Never commit API keys or sensitive data

### **Contribution Process**
1. Fork the repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

### **Issue Reporting**
- Use GitHub Issues for bug reports
- Include device information and Android version
- Provide steps to reproduce issues
- Attach screenshots when applicable

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 📞 Support & Contact

- **Repository**: [GitHub - RecyclableTrashClassification](https://github.com/BasakArghy/RecyclableTrashClassification)
- **Issues**: [GitHub Issues](https://github.com/BasakArghy/RecyclableTrashClassification/issues)
- **Owner**: BasakArghy

---

## 🙏 Acknowledgments

- **Google Teachable Machine** for AI model training platform
- **Firebase** for comprehensive backend services
- **Stripe** for secure payment processing
- **Material Design** for UI/UX guidelines
- **TensorFlow Lite** for mobile machine learning
- **Android Open Source Project** for development framework

---

*Last Updated: August 8, 2025*

**Happy Recycling! 🌱♻️**
