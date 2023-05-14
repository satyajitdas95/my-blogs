---
title: "Android Passkey: Enhancing Security and Ease for Signing In"
seoDescription: "Android Passkey: Public-key cryptography & biometric authentication for secure, convenient website & app sign-ins"
datePublished: Sun May 14 2023 13:21:56 GMT+0000 (Coordinated Universal Time)
cuid: clhng3qjr000009jwgya77t5m
slug: android-passkey-enhancing-security-and-ease-for-signing-in
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683990233995/b95e58a1-d120-4ed0-a91d-ffe3e8be75ce.gif
tags: security, android, google, passkeys

---

Do you ever forget your passwords? Or maybe you're worried about your passwords being stolen. If so, then you're not alone. Millions of people struggle with passwords every day.

But there's good news! There's a new way to sign in to websites and apps that is both easier and more secure than passwords. It's called Android passkeys.

## 1\. What is Android Passkey?

Android Passkeys are a more secure and convenient alternative to passwords, allowing users to sign in to apps and websites using biometric sensors, PINs, or patterns instead of traditional passwords.

Passkeys use cryptographic keys instead of strings of characters. This makes them much more secure than traditional passwords, which can be easily guessed or stolen.

## 2\. How does Android Passkey work?

Passkeys are based on public-key cryptography, which allows for secure authentication without the need to store any sensitive data on a server.

When you create a passkey, your device generates a unique public and private key pair. The public key is stored on the server, while the private key is kept secret on your device.

When you log in, the server sends a challenge to your device. Your device uses the private key to generate a response, which is then sent back to the server. If the response is correct, you are logged in.

Passkeys have several advantages over traditional passwords. First, they are much more secure. Because the private key is never stored on a server, it cannot be stolen or hacked.

Second, passkeys are much easier to use. You do not have to remember a long, complex password. Instead, you can simply use your fingerprint or facial recognition to log in.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684067895528/5214a2d4-c9f3-4189-af95-a61cfeeffc6c.webp align="center")

## 3\. What are the benefits of using Android Passkey?

* **They are more secure than passwords.** Passkeys use public-key cryptography, which makes them much more difficult to hack or steal than traditional passwords.
    
* **They are easier to use.** You do not have to remember a long, complex passkey. Instead, you can simply use your fingerprint or facial recognition to log in.
    
* **They are more portable.** Passkeys are stored on your device, so you can use them on any computer or device that supports them.
    
* **They are more future-proof.** Passwords are becoming increasingly obsolete. As more and more websites and apps adopt passkeys, it will become increasingly important to use them.
    

## **4\. How to Create an Android Passkey**

To use CredentialManager for generating a passkey, you can follow these steps:

1. Open your app and sign in to establish a session.
    
2. Next, your app prompts the user to create a passkey.
    
3. The system displays this UI near the bottom of the screen.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1684069457809/d5f37c6c-1e69-4556-8463-ee817cd90254.webp align="center")

1. A passkey is created after receiving the user's consent using the device's screen lock/biometrics. The credential provider creates a new asymmetric key pair and securely stores the private key on the device.
    
2. After the suspendable call is resolved, a public key credential containing a new public key, a credential ID, and other attestation data is returned to your app.
    

The example code shows how to create a passkey using [CredentialManager](https://developer.android.com/training/sign-in/passkeys#kotlin)

```kotlin
// Use your app or activity context to instantiate a client instance of
// CredentialManager.
val credentialManager = CredentialManager.create(context)

fun createPasskey(requestJson: String, preferImmediatelyAvailableCredentials: Boolean) {
    val createPublicKeyCredentialRequest = CreatePublicKeyCredentialRequest(
        // Contains the request in JSON format. Uses the standard WebAuthn
        // web JSON spec.
        requestJson = requestJson,
        // Defines whether you prefer to use only immediately available credentials,
        // not hybrid credentials, to fulfill this request. This value is false
        // by default.
        preferImmediatelyAvailableCredentials = preferImmediatelyAvailableCredentials,
    )
    // Execute CreateCredentialRequest asynchronously to register credentials
    // for a user account. Handle success and failure cases with the result and
    // exceptions, respectively.
    coroutineScope.launch {
        try {
            val result = credentialManager.createCredential(
                request = createPublicKeyCredentialRequest,
                activity = activity,
            )
            handlePasskeyRegistrationResult(result)
        } catch (e : CreateCredentialException){
            //handle error
        }
    }
}
```

Source: Google LLC. 2022

## **5\. What are some of the limitations of Android Passkey?**

* **Not all websites and apps support passkeys yet.** This is a rapidly developing technology, and more and more websites and apps are supporting passkeys all the time. However, there are still some that don't, so you may not be able to use passkeys everywhere.
    
* **Passkeys are not as secure as hardware security keys.** Hardware security keys are physical devices that you plug into your computer or phone when you log in to websites and apps. They offer an extra layer of security because they are not connected to the internet, so they cannot be hacked remotely. Passkeys are still very secure, but they are not as secure as hardware security keys.
    
* **Passkeys can be a bit of a hassle to set up.** You have to create a passkey for each website or app that you want to use. This can be a bit time-consuming, especially if you have a lot of accounts.
    

## **6\. The future of Android Passkey**

Google has been working on this technology for years, and it is finally starting to gain traction. More and more websites and apps are supporting passkeys, and it is only a matter of time before they become the standard way to log in to online accounts.

There are several reasons why passkeys are so promising. First, they are much more secure than traditional passwords. Passkeys use public-key cryptography, which makes them very difficult to hack or steal.

Second, passkeys are much easier to use than traditional passwords. You do not have to remember a long, complex password. Instead, you can simply use your fingerprint or facial recognition to log in.

As more and more people become aware of the benefits of passkeys, they are likely to become the standard way to log in to online accounts. This will make our online lives much more secure and convenient.

---

In conclusion, Android Passkeys offer a more secure and convenient alternative to traditional passwords for signing in to websites and apps. using public-key cryptography and biometric authentication.

Though not universally supported or as secure as hardware security keys, their adoption is growing, leading to a safer and user-friendly online experience.

If you enjoyed this blog, please give it a like and share it with others who may find it helpful.