Resources:

1) Root android device:

https://proandroiddev.com/root-an-android-emulator-avd-9f912328ca08

2) Download Frida and how to use:

https://labs.cognisys.group/posts/Writing-your-first-Frida-script-for-Android/

https://github.com/frida/frida/releases

3) Jadex download:

https://github.com/skylot/jadx/releases/tag/v1.5.1

4) PICOCTF - DROID

https://picoctf2019.haydenhousen.com/reverse-engineering

5) Beetlebug

https://medium.com/@68abdelrahmanmohamed/beetlebug-android-ctf-walk-through-19a18ffce9ad

6) DivaApplication

(i)  part 1: https://medium.com/@sudobro/diva-beta-android-app-walkthrough-4b0f114aa74

(ii) part 2: https://medium.com/@sudobro/diva-android-app-walkthrough-part-2-fbb50473cfb2

Commands:

---adb---

    database:
            -use App inspector
    
    shared_pref:
            -go to /data/data/app_name in device explorer
    
    external file:
            -go to /storage in device explorer
    
    strings:
            -use jadx, go to Resources/resource.arsc/res/values
    
    logging:
            -logcat
    
    sd-card:
            -allow permissions
            - go too /sdcard in device explorer
    
    SQLI : ' OR '1'='1' -- (most common way)
    
    ADB use case:
            -start an exported activity:
                     adb shell am start -n activity_name (example: app.beetlebug/.ctf.b33tleAdministrator) 
            -start an exported service:
                    adb shell am startservice -n service_name (example: app.beetlebug/.handlers.VulnerableService)
            -access a content provider:
                     adb shell content query --uri query_content (example: content://app.beetlebug.provider/users)

        
---apktool---
        
        # Re-compile the app
        
        apktool d three.apk --no-res
        
        # three is the base folder of the decompiled app
        
        apktool b three
        
        # Change directory to the newly generated APK
        cd three/dist
        
        # Generate a new key to sign the build
        keytool -genkeypair -v -keystore key.keystore -alias publishingdoc -keyalg RSA -keysize 2048 -validity 10000
        
        # Sign the new build
        jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore ./key.keystore three.apk publishingdoc
        
        # Uninstall previous version of the app and install the new one
        adb uninstall com.hellocmu.picoctf 
        adb install three.apk
        
        https://picoctf2019.haydenhousen.com/reverse-engineering/droids3
