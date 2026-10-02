# Fintech Wallet App

> Complete cross-platform digital wallet built with **React Native CLI** + TypeScript.

![React Native](https://img.shields.io/badge/React_Native-0.79.7-61DAFB?logo=react)
![TypeScript](https://img.shields.io/badge/TypeScript-5.x-blue)
![Biometrics](https://img.shields.io/badge/Biometrics-supported-green)
![Secure Storage](https://img.shields.io/badge/Keychain%2FKeystore-secured-orange)

## Overview

A production-minded mobile wallet that demonstrates real-world fintech patterns:

- Biometric authentication (Fingerprint / Face ID)
- QR code payments
- Transaction history
- Offline mode + background sync
- Encrypted API communication
- Real-time updates via WebSocket
- Secure token storage using Keychain / Keystore

## Architecture

┌─────────────────────────────────────────────┐
│                 UI Layer                    │
│  Screens (Login, Home, QR, History, etc.)   │
└─────────────────────┬───────────────────────┘
                      │
┌─────────────────────▼───────────────────────┐
│              State / Hooks                  │
│         (React Context + Custom Hooks)      │
└─────────────────────┬───────────────────────┘
                      │
┌─────────────────────▼───────────────────────┐
│               Services Layer                │
│  • AuthService (Biometrics + Tokens)        │
│  • ApiService (Axios + Interceptors)        │
│  • SecureStorage (Keychain)                 │
│  • OfflineQueue + Sync                      │
│  • WebSocketService                         │
└─────────────────────┬───────────────────────┘
                      │
         ┌────────────┼────────────┐
         ▼            ▼            ▼
   Backend API   Secure Store   WebSocket

### Key Design Decisions

| Decision | Why | Trade-off |
|----------|-----|---------|
| React Native CLI | Full native module access & better performance control | More setup than Expo |
| react-native-keychain | Industry-standard secure storage | Platform-specific configuration needed |
| react-native-biometrics | Native biometric prompts | Requires device support |
| Offline queue | Better UX in poor network conditions | Conflict resolution complexity |
| Axios interceptors | Centralized auth & error handling | Slight learning curve |

## Tech Stack

- **Framework:** React Native CLI 0.75+
- **Language:** TypeScript
- **Navigation:** React Navigation 6
- **Networking:** Axios
- **Secure Storage:** react-native-keychain
- **Biometrics:** react-native-biometrics
- **QR:** react-native-qrcode-svg + react-native-camera (or vision-camera)
- **Real-time:** socket.io-client
- **State:** React Context + useReducer (can be upgraded to Zustand/Redux later)

## Prerequisites

- Node.js >= 18
- JDK 17
- Android Studio (Android SDK + Emulator)
- Xcode + CocoaPods (for iOS)
- React Native environment set up ([official guide](https://reactnative.dev/docs/environment-setup))

## Getting Started

```bash
# Clone the repository
git clone https://github.com/olabodeIdowu/fintech-wallet-app.git
cd fintech-wallet-app

# Install dependencies
yarn install
# or npm install

# iOS only
cd ios && pod install && cd ..

# Start Metro
yarn start

# Run on Android
yarn android

# Run on iOS
yarn ios

Project Structure

src/
├── components/
├── screens/
│   ├── LoginScreen.tsx
│   ├── HomeScreen.tsx
│   ├── QRPaymentScreen.tsx
│   ├── TransactionHistoryScreen.tsx
│   └── ...
├── navigation/
│   └── AppNavigator.tsx
├── services/
│   ├── api.ts
│   ├── secureStorage.ts
│   ├── auth.ts
│   ├── offlineQueue.ts
│   └── websocket.ts
├── hooks/
├── context/
│   └── AuthContext.tsx
├── types/
├── utils/
└── App.tsx

Features ImplementedBiometric login with fallback
Secure JWT storage
Protected routes
QR code generation & scanning (payment flow)
Transaction list with pull-to-refresh
Offline action queue + automatic sync when back online
Real-time balance/transaction updates via WebSocket
Clean error handling and loading states

What I OwnedComplete mobile architecture
Secure authentication flow
Offline-first patterns
Real-time integration
Native module integration (biometrics + secure storage)
Clean separation of UI / services / state

Security NotesTokens never stored in AsyncStorage
All sensitive data goes through Keychain / Keystore
Certificate pinning can be added easily
Biometric prompt is required before accessing the wallet

Future ImprovementsFull end-to-end encryption for messages
Push notifications (FCM / APNs)
Multi-currency support
Transaction category analytics
Deep linking for payment requests
Detox / Maestro E2E tests

