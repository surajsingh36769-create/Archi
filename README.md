# ARCHICRETE.IN - Employee Attendance & Salary Management System

A comprehensive, cross-device employee attendance and salary management system built with React, TypeScript, and Firebase.

## 🌟 Features

### Core Features
- ✅ **GPS-based Attendance** - 50-meter geofence verification using Haversine formula
- ✅ **Selfie-based Check-in/Check-out** - Camera capture with face verification
- ✅ **Multi-device Support** - Sync data across all devices using Firebase
- ✅ **Role-based Access** - Separate interfaces for Managers and Employees
- ✅ **Real-time Dashboard** - Live attendance statistics and charts
- ✅ **Salary Calculation** - Configurable monthly/daily/hourly salary with overtime
- ✅ **Leave Management** - Employee leave requests with manager approval
- ✅ **Holiday Management** - Company holiday calendar
- ✅ **Attendance Reports** - Export to CSV/Excel/PDF
- ✅ **Audit Logs** - Track all attendance modifications

### Cross-Device Features
- 🔄 **Firebase Cloud Sync** - Real-time data synchronization across devices
- 📱 **Mobile-first Design** - Optimized for Android/iOS phones
- 💻 **Desktop Dashboard** - Full-featured manager interface
- 📊 **QR Code Location** - Share factory location via QR code
- 💾 **Data Export/Import** - Manual backup and restore

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ and npm
- Firebase account (free tier is sufficient)

### Installation

1. **Clone and Install**
```bash
npm install
```

2. **Start Development Server**
```bash
npm run dev
```

3. **Build for Production**
```bash
npm run build
```

## 🔥 Firebase Setup (For Multi-Device Sync)

### Step 1: Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Click "Add Project"
3. Enter project name (e.g., "archicrete-attendance")
4. Disable Google Analytics (optional)
5. Click "Create Project"

### Step 2: Enable Firestore Database

1. In Firebase Console, go to **Build → Firestore Database**
2. Click "Create database"
3. Select "Start in test mode" (for development)
4. Choose your location
5. Click "Enable"

### Step 3: Configure Security Rules

For **development/testing**, use these rules:
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

For **production**, use more restrictive rules:
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.time < timestamp.date(2025, 12, 31);
    }
  }
}
```

### Step 4: Register Web App

1. In Firebase Console, go to **Project Settings** (gear icon)
2. Scroll to "Your apps" section
3. Click the Web icon (</>)
4. Enter app nickname (e.g., "ARCHICRETE Web")
5. Check "Also set up Firebase Hosting" (optional)
6. Click "Register app"
7. **Copy the configuration values** (you'll need these next)

### Step 5: Connect in Application

1. Open the application and login as Manager
   - Username: `admin`
   - Password: `admin123`

2. Go to **Settings → Cloud Sync**

3. Paste your Firebase configuration:
   - **API Key**: `AIzaSy...`
   - **Auth Domain**: `your-project.firebaseapp.com`
   - **Project ID**: `your-project-id`
   - **Storage Bucket**: `your-project.appspot.com`
   - **Messaging Sender ID**: `123456789`
   - **App ID**: `1:123456789:web:abc123`

4. Click **"Connect to Firebase"**

5. Once connected, click **"Push to Cloud"** to upload your data

### Step 6: Sync Other Devices

On each additional device:

1. Open the application
2. Login with any account
3. Go to **Settings → Cloud Sync**
4. Enter the same Firebase configuration
5. Click **"Connect to Firebase"**
6. Click **"Load from Cloud"** to download the data
7. The application will reload with synced data

## 📱 Usage Guide

### For Managers

#### Initial Setup
1. **Configure Factory Location**
   - Go to Settings → Factory
   - Stand at factory location
   - Click "Use Current Location"
   - Save settings

2. **Add Employees**
   - Go to Employees → Add Employee
   - Fill in employee details
   - Set salary type (monthly/daily/hourly)
   - Save

3. **Configure Attendance Rules**
   - Go to Settings → Attendance
   - Set shift timings
   - Configure overtime rules
   - Save

4. **Setup Firebase** (for multi-device)
   - Go to Settings → Cloud Sync
   - Follow Firebase setup guide
   - Push data to cloud

#### Daily Operations
- **View Dashboard**: See real-time attendance statistics
- **Manage Attendance**: View/correct attendance records
- **Approve Leaves**: Review and approve employee leave requests
- **Generate Reports**: Export attendance and salary reports
- **Sync Data**: Push changes to cloud for other devices

### For Employees

#### Daily Attendance
1. **Open Application** on your phone
2. **Login** with your credentials
   - Username: Your Employee ID (e.g., EMP001)
   - Password: `emp123` (default)

3. **Check In**
   - Click "CHECK IN" button
   - Allow location permission
   - Verify you're within 50m of factory
   - Take selfie
   - Confirm check-in

4. **Check Out**
   - Click "CHECK OUT" button
   - Allow location permission
   - Take selfie
   - Confirm check-out

#### View Records
- **Attendance History**: View past attendance records
- **Salary Details**: View monthly salary breakdown
- **Profile**: View personal information

## 🔐 Demo Credentials

### Manager Account
- **Username**: `admin`
- **Password**: `admin123`

### Employee Accounts
- **Username**: `EMP001` to `EMP005`
- **Password**: `emp123`

## 📊 Data Structure

### Collections (Firestore)
- `employees` - Employee records
- `attendance` - Daily attendance records
- `holidays` - Company holidays
- `leaves` - Leave requests
- `settings` - Factory and system settings
- `users` - User accounts

### Local Storage Keys
- `archicrete_employees`
- `archicrete_attendance`
- `archicrete_holidays`
- `archicrete_leaves`
- `archicrete_settings`
- `archicrete_users`
- `firebase_config`

## 🛠️ Configuration

### Factory Settings
- **Location**: Latitude/Longitude coordinates
- **Radius**: Attendance geofence (default: 50m)
- **Shift Timings**: Start and end times
- **Grace Period**: Late arrival tolerance
- **Break Duration**: Unpaid break time
- **Overtime Threshold**: When overtime starts

### Salary Settings
- **Monthly Salary**: Fixed monthly amount
- **Daily Salary**: Per-day rate
- **Hourly Rate**: Per-hour rate
- **Overtime Multiplier**: OT pay multiplier (default: 1.5x)
- **Working Days**: Days per month (default: 26)

## 🔄 Sync Workflow

### Primary Device (Manager's Desktop)
1. Make changes (add employees, correct attendance, etc.)
2. Go to Settings → Cloud Sync
3. Click "Push to Cloud"
4. Data is uploaded to Firebase

### Secondary Devices (Employee Phones, Other Computers)
1. Open application
2. Go to Settings → Cloud Sync
3. Click "Load from Cloud"
4. Application reloads with latest data
5. Continue working

### Best Practices
- **Sync Daily**: Push changes at end of each day
- **Backup Regularly**: Use Data Sync → Export as backup
- **Test Location**: Use QR code to verify factory location
- **Monitor Sync**: Check "Last Sync" timestamp

## 🐛 Troubleshooting

### Location Not Working
- Ensure GPS/location services are enabled
- Allow browser location permission
- Check factory coordinates are correct
- Use QR code to verify location on map

### Firebase Connection Failed
- Verify all config values are correct
- Check Firestore database is enabled
- Verify security rules allow access
- Check browser console for errors

### Data Not Syncing
- Ensure all devices use same Firebase project
- Push from primary device first
- Load on secondary devices
- Check "Last Sync" timestamp

### Camera Not Working
- Allow camera permission in browser
- Check camera is not in use by another app
- Try a different browser
- Use HTTPS (required for camera access)

## 📱 Browser Compatibility

### Supported Browsers
- ✅ Chrome 90+ (Desktop & Mobile)
- ✅ Safari 14+ (iOS & macOS)
- ✅ Firefox 88+ (Desktop)
- ✅ Edge 90+ (Desktop)

### Required Features
- Geolocation API
- Camera API (getUserMedia)
- LocalStorage
- Firebase SDK

## 🔒 Security Notes

### Firebase Security
- Use restrictive security rules in production
- Consider Firebase Authentication for user verification
- Enable Firestore security rules validation
- Monitor Firestore usage in Firebase Console

### Application Security
- Passwords are stored in plain text (demo only)
- For production, implement proper authentication
- Use HTTPS for all deployments
- Never commit Firebase config to public repos

### Data Privacy
- Employee selfies are stored locally
- Location data is used only for attendance verification
- No data is sent to third-party servers (except Firebase)
- Employees can view their own data only

## 📈 Future Enhancements

- [ ] Firebase Authentication integration
- [ ] Real-time attendance updates
- [ ] Push notifications for managers
- [ ] Biometric authentication
- [ ] Offline mode with sync queue
- [ ] Advanced reporting and analytics
- [ ] Employee self-service portal
- [ ] Mobile app (React Native)
- [ ] Integration with biometric devices
- [ ] Multi-language support

## 📄 License

This is a proprietary application for ARCHICRETE.IN

## 🤝 Support

For issues or questions:
1. Check the troubleshooting section
2. Review Firebase setup guide
3. Check browser console for errors
4. Verify all configurations are correct

## 🎯 Key Technologies

- **Frontend**: React 18 + TypeScript
- **Styling**: Tailwind CSS
- **Charts**: Recharts
- **Icons**: Lucide React
- **Database**: Firebase Firestore
- **Build Tool**: Vite
- **Routing**: React Router

---

**Built with ❤️ for ARCHICRETE.IN**
