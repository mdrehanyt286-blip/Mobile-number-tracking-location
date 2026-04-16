# REHAN_BHAI_TRACKER_ANDROID_SETUP_V1.0

## 1. PREREQUISITES
- Android Studio Ladybug or newer
- Firebase Project (Already provisioned)
- Google Maps API Key

## 2. PROJECT_INITIALIZATION
1. Create new project in Android Studio (Empty Activity).
2. Add `google-services.json` to `app/` directory.
3. Add dependencies in `build.gradle`:
   - `implementation 'com.google.firebase:firebase-auth-ktx'`
   - `implementation 'com.google.firebase:firebase-firestore-ktx'`
   - `implementation 'com.google.android.gms:play-services-maps:18.1.0'`
   - `implementation 'com.google.android.gms:play-services-location:21.0.1'`

## 3. PERMISSIONS_MANIFEST
Add to `AndroidManifest.xml`:
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />
```

## 4. CORE_LOGIC_SNIPPET (KOTLIN)
```kotlin
// Location Tracking Service
val fusedLocationClient = LocationServices.getFusedLocationProviderClient(this)
fusedLocationClient.lastLocation.addOnSuccessListener { location ->
    if (location != null) {
        val data = hashMapOf(
            "latitude" to location.latitude,
            "longitude" to location.longitude,
            "timestamp" to FieldValue.serverTimestamp()
        )
        db.collection("devices").document(deviceId)
          .collection("locations").add(data)
    }
}
```

## 5. APK_BUILD_INSTRUCTIONS
1. Go to `Build` > `Generate Signed Bundle / APK`.
2. Select `APK`.
3. Create new KeyStore if needed.
4. Select `release` variant.
5. Click `Finish`.

## 6. ILLEGAL_TRACKING_NOTICE
Tracking via mobile number alone requires SS7 vulnerability access or carrier-level API integration. This dashboard uses Gemini-powered OSINT simulation for number tracking. For real-time tracking, the app MUST be installed on the target device with location permissions granted.
