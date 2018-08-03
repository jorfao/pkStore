# pkStore
Emulator platform keystore, suitable for testing system apps. Default keys sourced from [AOSP](https://github.com/aosp-mirror/platform_build/tree/master/target/product/security). You can use the provided keystore to test system apps on emulator or create your own by following the instructions below.

**Doesn't work on images with Google API's**


## Steps to create a platform.keystore:

###### Convert PK8 to PEM KEY
openssl pkcs8 -inform DER -nocrypt -in <platform.pk8> -out <platform.pem>

###### Bundle CERT and KEY
openssl pkcs12 -export -in <platform.x509.pem> -inkey <platform.pem> -out <platform.pk1>2 -password pass:<android> -name <android>
  
###### Import P12 in Keystore
keytool -importkeystore -deststorepass <android> -destkeystore <platform.keystore> -srckeystore <platform.pk12> -srcstoretype PKCS12 -srcstorepass <android>
