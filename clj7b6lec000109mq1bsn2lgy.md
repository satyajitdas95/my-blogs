---
title: "Blockstore: Hassle-Free Account Migration"
seoTitle: "Blockstore: Effortless Account Transfer"
seoDescription: "Blockstore: Secure, encrypted Android account migration for improved user experience and app retention"
datePublished: Thu Jun 22 2023 15:39:17 GMT+0000 (Coordinated Universal Time)
cuid: clj7b6lec000109mq1bsn2lgy
slug: blockstore-hassle-free-account-migration
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1687448067980/ffa7dbd6-d049-49c3-a082-cd188bedf84c.png
tags: android-app-development, android, kotlin, blockstore, androidmigration

---

Whenever you purchase a new Android device and upgrade from an older one, you typically migrate all your data, such as images, contacts, and even previously installed apps.

However, the real challenge begins when you attempt to use an app and have to log in. In some cases, it's more than just a simple login. Users may forget their login email, username, or password.

In today's digital world, people use different passwords for various purposes, which can lead to confusion. This issue sometimes results in users either creating a new account or abandoning the app altogether.

Block Store can solve this problem. The Block Store API aims to make logging back into users' applications on a new device as simple as restoring from a backup during the setup process.

This allows users to return to their apps just as they left them. Read on to learn more about Block Store, its benefits, and how to provide users with a seamless experience!

## How BlockStore Works?

Blockstore is a Google Play Services API that allows developers to store and restore small amounts of data on an Android device. This data can be anything important to the current user session, such as an authentication token, a user preference, or a small piece of file data.

Blockstore data is stored in an encrypted file on the device. This file is only accessible to the app that created it, and it cannot be accessed by other apps.

When a user signs into your app, you can save their authentication token to Blockstore. This token will then be stored on the device and will be available when the user signs in again on a different device.

Blockstore data can also be used to transfer data between devices. For example, if a user has your app installed on two devices, you can use Blockstore to transfer their user preferences from one device to the other.

This allows for a seamless user experience, as the user will not have to re-enter their preferences when they switch devices.

Here is how Blockstore works in more detail:

1. When a developer wants to store data in Blockstore, they call the `putBytes()` method. This method takes two parameters: the data to be stored, and a unique identifier for the data.
    
2. The `putBytes()` the method encrypts the data and stores it in the Blockstore file. The unique identifier is used to associate the data with the app that created it.
    
3. When a developer wants to retrieve data from Blockstore, they call the `retrieveBytes()` method. This method takes the unique identifier for the data as a parameter and returns the encrypted data.
    
4. The developer can then decrypt the data and use it as they see fit.
    

Example of Saving a Token -

```kotlin
 val client = Blockstore.getClient(this)

  val bytes1 = byteArrayOf(1, 2, 3, 4) // Store one data block.
  val key1 = "com.example.app.key1"
  val storeRequest1 = StoreBytesData.Builder()
    .setBytes(bytes1) // Call this method to set the key value with which the data should be associated with.
    .setKeys(Arrays.asList(key1))
    .build()
  client.storeBytes(storeRequest1)
    .addOnSuccessListener { result: Int ->
      Log.d(TAG,
            "Stored $result bytes")
    }
  .addOnFailureListener { e ->
      Log.e(TAG, "Failed to store bytes", e)
    }
```

Source: 2021 Google LLC.

Example of retrieving a token -

```kotlin
val client = Blockstore.getClient(this)

// Retrieve data associated with certain keys.
val key1 = "com.example.app.key1"
val key2 = "com.example.app.key2"
val key3 = BlockstoreClient.DEFAULT_BYTES_DATA_KEY // Used to retrieve data stored without a key

val requestedKeys = Arrays.asList(key1, key2, key3) // Add keys to array

val retrieveRequest = RetrieveBytesRequest.Builder()
  .setKeys(requestedKeys)
  .build()

client.retrieveBytes(retrieveRequest)
  .addOnSuccessListener { result: RetrieveBytesResponse ->
    val blockstoreDataMap =
      result.blockstoreDataMap
    for ((key, value) in blockstoreDataMap) {
      Log.d(ContentValues.TAG, String.format(
        "Retrieved bytes %s associated with key %s.",
        String(value.bytes), key))
    }
  }
  .addOnFailureListener { e: Exception? ->
    Log.e(ContentValues.TAG,
          "Failed to store bytes",
          e)
  }
```

Source: 2021 Google LLC.

---

In conclusion, Blockstore offers a seamless and secure solution for storing and transferring app-specific data on Android devices.

By leveraging this API, developers can enhance user experience and reduce the hassle of logging in or setting up preferences across multiple devices. As users increasingly rely on multiple devices, integrating Blockstore into your app can significantly improve user satisfaction and retention.

That's all for now. To learn more check out the [documentation](https://developers.google.com/identity/blockstore/android).

If you enjoyed the article, please give it a thumbs up. Happy coding!