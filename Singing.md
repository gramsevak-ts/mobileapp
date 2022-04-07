# Signign gsts-govt.apk

After a successfull build of unsigned apk,we should sign our apk using apksigner. For that we need to generate a private key using keytool

```
keytool -genkey -v -keystore gsts-govt-release-key.jks -keyalg RSA -keysize 2048 -validity 36500 -alias gsts-govt
```
The above command prompts us for passwords for the keystore and key, and for the "Distinguished Name" fields for key.

It then generates the keystore as a file called gsts-govt-release-key.jks.
 
Following are the given field names and credentials used while signing gsts-govt.apk

keystore password:
```.

Enter keystore password:  1!Qshadkona
```
What is your first and last name?
```
DevOps
```
What is the name of your organization?
```
Shadkona Technologies Private Limited
```
What is the name of your City or Locality?
```
Hyderabad
```
What is the name of your State or Province?
```
Telangana
```
What is the two-letter country code for this unit?
```
IN
```
Is CN=GramSevak Telangana, OU=DevOps, O=Shadkona Technologies Private Limited, L=Hyderabad, ST=Telangana, C=IN correct?
  [no]:  yes
  
  Generating 2,048 bit RSA key pair and self-signed certificate (SHA256withRSA) with a validity of 36,500 days
	for: CN=GramSevak Telangana, OU=DevOps, O=Shadkona Technologies Private Limited, L=Hyderabad, ST=Telangana, C=IN
[Storing gsts-govt-release-key.jks]

Now we can sign APK using the gsts-govt-release-key.jks.

Align the unsigned APK using zipalign: 

```
zipalign -v -p 4 app-release-unsigned.apk gsts-govt-unsigned-aligned.apk
```
zipalign ensures that all uncompressed data starts with a particular byte alignment relative to the start of the file, which may reduce the amount of RAM consumed by an app. 

Sign your APK with your private key using apksigner: 
```
apksigner sign --ks gsts-govt-release-key.jks --out gsts-govt.apk gsts-govt-unsigned-aligned.apk
```
It prompts for keystore password.

After successfully signing the apk file, Our unsigned apk app-release-unsigned.apk will be signed and as a result gsts-govt.apk file will be created and placed in /app/build/outputs/apk/release

Verify that your APK is signed: 
```
apksigner verify gsts-govt.apk
```
