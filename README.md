Secure Comms - Tactical Communication Suite

Secure Comms is a high-security, Flutter-based mobile application designed for tactical operations and secure data exchange. Developed as a final-year engineering project, it integrates military-grade communication protocols, native WireGuard® VPN tunneling, and a suite of security utilities into a single, cohesive interface.

The application features a "Mission Mode" for high-contrast tactical usage, rank-based channel access (Operative, Officer, Commander), and secure file sharing capabilities.

🚀 Key Features

1. Secure Communication

Real-time Messaging: Powered by Google Firestore for instant data sync.

Military Structure: Create Unit Channels (Group Chat) or Broadcast Channels (One-way command alerts).

Rank-Based Access: Channels can be restricted by rank (Lvl 1 Operative, Lvl 2 Officer, Lvl 3 Commander). Lower ranks cannot view high-clearance channels.

Secure File Sharing: Upload and send PDFs, Docs, and Images securely via Firebase Storage.

"Once View" Messages: Send sensitive messages that lock permanently after being viewed by the recipient.

2. Integrated VPN

Native WireGuard® Implementation: Uses the modern, high-speed WireGuard protocol.

Real-time Statistics: Monitors upload/download speeds and connection duration.

Network Analysis: Detects network type (WiFi/5G) and security encryption level (WPA2/AES).

3. Security Tools

Password Generator: Create cryptographically strong passwords with custom rules (length, symbols, etc.).

Password Strength Checker: Real-time analysis of password complexity.

Secure PDF Viewer: (WebView Integrated) Interface for viewing self-destructing/encrypted PDFs hosted on a private server.

Link Analyzer: (WebView Integrated) Interface for scanning URLs for threats via a backend service.

4. Advanced UI/UX

Glassmorphism Design: Modern, translucent UI elements with blur effects.

Adaptive Themes:

Light/Dark Mode: Standard professional themes.

Mission Mode: High-contrast Red/Black tactical theme for low-light environments.

🛠️ Tech Stack

Framework: Flutter (Dart)

Backend: Firebase (Auth, Firestore, Storage)

VPN Protocol: WireGuard (via wireguard_flutter)

State Management: Provider

Animations: Lottie

⚙️ Configuration Guide

To run this project yourself, you need to configure the VPN keys and the Firebase backend.

1. Configure the VPN (WireGuard)

The app is hardcoded to use a specific WireGuard configuration. You must update this with your own credentials (from your VPS or a provider like ProtonVPN).

Get your Config: Obtain a standard .conf file from your VPN provider. It will contain a PrivateKey, Address, DNS, PublicKey, and Endpoint.

Open the Code: Navigate to lib/main.dart.

Find the Function: Search for the toggleVpn method inside the AppState class (approx. line 500-550).

Update the Variable: Look for the String wgConfig variable. Replace the text inside the triple quotes """ with your config.

// lib/main.dart

void toggleVpn() async {
  // ...
  try {
    // --- PASTE YOUR CONFIG HERE ---
    String wgConfig = """
[Interface]
PrivateKey = <YOUR_PRIVATE_KEY>
Address = 10.2.0.2/32
DNS = 10.2.0.1

[Peer]
PublicKey = <YOUR_SERVER_PUBLIC_KEY>
AllowedIPs = 0.0.0.0/0
Endpoint = <YOUR_SERVER_IP>:51820
""";
    // ...


2. Configure Firebase

You need your own Firebase project to handle users and chats.

A. Console Setup

Go to the Firebase Console.

Create a Project.

Authentication: Go to Build > Authentication. Click "Get Started" and enable Email/Password.

Firestore Database: Go to Build > Firestore Database. Click "Create Database". Start in Test Mode (or Production mode, but update Rules to allow read/write).

Storage: Go to Build > Storage. Click "Get Started". Start in Test Mode.

B. App Registration

Android: Add an Android app. Download google-services.json and place it in android/app/.

iOS: Add an iOS app. Download GoogleService-Info.plist and place it in ios/Runner/.

Web: Add a Web app. Copy the firebaseConfig object keys.

Open lib/main.dart.

Find const FirebaseOptions webFirebaseOptions (at the top of the file).

Replace the apiKey, appId, etc., with your own keys.

3. Configure External Tools (PDF/Link Analyzer)

The "Secure PDF" and "Link Analyzer" tools use WebView to display external tools hosted on your local network or a server.

Open lib/tools/secure_pdf_tool.dart and lib/tools/link_analyzer_tool.dart.

Find the _serverUrl variable in the state class.

Update the IP address (e.g., http://192.168.1.5:5000) to point to your running Python/Flask server.

📖 User Guide

How to Add Users & Chat

Sign Up: Use the "Sign Up" button on the login screen. You can select your Rank (Operative, Officer, Commander) here.

Start a Chat: Go to the "Chats" tab and tap the + button.

Search: Go to the "Direct Message" tab and search for another user by their exact email address.

Create a Group: Go to the "Create Channel" tab, search/select multiple users, give the channel a name, and set a Minimum Rank.

Note: If you set Min Rank to "Commander", users signed up as "Operative" will not see this channel.

How to Use "Once View" Messages

In a chat, tap the Unlock Icon 🔓 next to the text field.

It will turn Red (Locked) 🔒.

Type and send your message.

The message is hidden. The recipient taps "Tap to View".

Once viewed, the message permanently changes to "Message Expired" for both parties.

How to Use Mission Mode

On the "Chats" screen, toggle the Mission Mode switch in the top right.

Effect: The entire app theme switches to High-Contrast Red/Black (Tactical Theme) for low-light usage.

Developer Settings (Rank Changer)

If you need to change your rank for testing:

Go to the Settings tab.

Tap the "App Version" list tile 3 times.

A hidden "Developer Settings" screen will appear where you can force-update your rank.


📦 Installation

# Clone the repository
git clone [https://github.com/yourusername/secure-comms.git](https://github.com/yourusername/secure-comms.git)

# Install dependencies
flutter pub get

# Run on Android Emulator (Recommended)
flutter run

Project by Satvik Trivedi, Final Year Engineering Project
