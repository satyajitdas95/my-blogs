---
title: "Exploring the OkHttp Interceptor"
seoTitle: "OkHttp Interceptor Guide"
seoDescription: "Explore OkHttp Interceptor's potential in Android development for logging, authentication, caching, and error handling, boosting app performance"
datePublished: Mon Jun 19 2023 13:58:02 GMT+0000 (Coordinated Universal Time)
cuid: clj2x8txc000109mj8bxk44ji
slug: exploring-the-okhttp-interceptor
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1687182803455/893ff601-28d4-4dc2-b225-ee5a80637a69.png
tags: android, kotlin, networking, okhttp, http-interceptor

---

In the world of Android development, networking is an essential part of building robust and feature-rich applications. OkHttp, a popular open-source HTTP client library, simplifies network operations and offers powerful features.

One such feature is interceptors, which allow developers to modify and observe HTTP requests and responses. In this blog post, we will explore interceptors in OkHttp and understand how they can be used effectively in Android applications.

## What are Interceptors?

An interceptor in OkHttp is a powerful mechanism that sits between the application and the network. It intercepts and modifies HTTP requests and responses, enabling developers to perform various tasks like logging, authentication, caching, and more.

> ***According to documentation, Interceptors are a powerful mechanism that can monitor, rewrite, and retry the API call. So basically, when we do some API call, we can monitor the call or perform some tasks.***

It acts as a middleware, providing a way to intercept and manipulate network communication without modifying the existing codebase.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687181734224/a46dfdcd-6c76-44cc-936c-25e5bdc8f8d8.png align="center")

Working Principle: When an HTTP request is made using OkHttp, interceptors come into action. OkHttp allows you to add interceptors to the client, which will be executed in the order they are added.

Each interceptor has the opportunity to inspect and modify the request before it is sent to the server and the response before it reaches the application.

Types of Interceptors: OkHttp provides two types of interceptors: application interceptors and network interceptors.

1. Application Interceptors: Application interceptors work on the application layer and have access to both the request and response. They are ideal for tasks like adding headers, logging, request/response modification, and authentication. These interceptors are executed first, allowing them to observe the entire network interaction.
    
2. Network Interceptors: Network interceptors operate on the network layer and have access to the raw network response. They are useful for tasks like caching, transparently decompressing responses, and rewriting responses. Network interceptors are executed after the application interceptors, enabling them to modify the response coming from the server.
    

Using Interceptors in OkHttp: To use interceptors in your OkHttp client, follow these steps:

1. Create an Interceptor: First, create a class that implements the `Interceptor` interface. This class will define the logic you want to execute when the interceptor intercepts a request or response.
    
2. Implement Interceptor Logic: Inside the interceptor class, override the `intercept` method. This method receives an `Chain` object that allows you to access and modify the request and response.
    
3. Add Interceptors to the OkHttp Client: Create an OkHttp `OkHttpClient` instance and add your interceptors using the `addInterceptor` or `addNetworkInterceptor` methods. Application interceptors should be added using, and network interceptors should be added using `addNetworkInterceptor`.
    
4. Make HTTP Requests: With the interceptors added to the client, you can now make HTTP requests using OkHttp as usual. The interceptors will automatically intercept the requests and responses, executing the logic you defined.
    

---

**Here are a few examples of what you can do with interceptors in Kotlin using the OkHttp library:**

## Logging Interceptor:

You can create an interceptor that logs the details of your network requests and responses.

This can help debug or monitor network activity. You can log information like request method, URL, headers, and response code.

```kotlin
val loggingInterceptor = HttpLoggingInterceptor().apply {
    level = HttpLoggingInterceptor.Level.BODY
}

val client = OkHttpClient.Builder()
    .addInterceptor(loggingInterceptor)
    .build()
```

## Authentication Interceptor:

This interceptor can be used to add authentication headers to your requests. For example, if your API requires an access token, you can check if the token is present in the request and add it if needed. If the token is expired, you can refresh it and retry the request.

```kotlin
val authInterceptor = Interceptor { chain ->
    val originalRequest = chain.request()
    val authenticatedRequest = originalRequest.newBuilder()
        .header("Authorization", "<your_access_token>")
        .build()
    chain.proceed(authenticatedRequest)
}

val client = OkHttpClient.Builder()
    .addInterceptor(authInterceptor)
    .build()
```

## Header Interceptor:

You can use this interceptor to add or modify headers in your requests. This can be useful for adding custom headers required by your server, such as API keys or user agent information.

```kotlin
val headerInterceptor = Interceptor { chain ->
    val originalRequest = chain.request()
    val modifiedRequest = originalRequest.newBuilder()
        .header("Custom-Header", "value")
        .build()
    chain.proceed(modifiedRequest)
}

val client = OkHttpClient.Builder()
    .addInterceptor(headerInterceptor)
    .build()
```

## Caching Interceptor:

This interceptor can implement caching strategies. You can intercept the responses and cache them locally based on specific criteria like response headers or URLs.

This can improve performance by reducing network requests for resources that are already cached.

```kotlin
val cache = Cache(context.cacheDir, CACHE_SIZE)

val cacheInterceptor = Interceptor { chain ->
    val originalResponse = chain.proceed(chain.request())
    val cacheControl = originalResponse.header("Cache-Control")

    if (cacheControl == null || cacheControl.contains("no-store") ||
        cacheControl.contains("no-cache") || cacheControl.contains("must-revalidate") ||
        cacheControl.contains("max-age=0")
    ) {
        originalResponse.newBuilder()
            .header("Cache-Control", "public, max-age=${CACHE_MAX_AGE}")
            .build()
    } else {
        originalResponse
    }
}

val client = OkHttpClient.Builder()
    .addNetworkInterceptor(cacheInterceptor)
    .cache(cache)
    .build()
```

## Offline Mode Interceptor:

You can create an interceptor that checks if the device is offline and returns cached responses instead of making network requests. This can help your app work offline by serving data from the cache when there is no internet connectivity.

```kotlin
val offlineInterceptor = Interceptor { chain ->
    var request = chain.request()
    if (!isOnline()) {
        request = request.newBuilder()
            .header("Cache-Control", "public, only-if-cached")
            .build()
    }
    chain.proceed(request)
}

val client = OkHttpClient.Builder()
    .addInterceptor(offlineInterceptor)
    .build()

// Helper method to check network connectivity
fun isOnline(): Boolean {
    val connectivityManager = getSystemService(Context.CONNECTIVITY_SERVICE) as ConnectivityManager
    val networkInfo = connectivityManager.activeNetworkInfo
    return networkInfo != null && networkInfo.isConnected
}
```

## Error Handling Interceptor:

This interceptor can handle specific HTTP error codes and perform actions accordingly. For example, if you receive a 401 Unauthorized response, you can automatically redirect the user to the login screen.

```kotlin
val errorInterceptor = Interceptor { chain ->
    val response = chain.proceed(chain.request())
    if (!response.isSuccessful && response.code == 401) {
        // Handle 401 Unauthorized error here
        // For example, redirect the user to the login screen
    }
    response
}

val client = OkHttpClient.Builder()
    .addInterceptor(errorInterceptor)
    .build()
```

## **Rewriting Responses**

Interceptors can modify the headers of a response and change the content of the response itself. However, this action can be riskier compared to modifying request headers because it might go against what the web server expects.

In challenging situations, if you are willing to accept the potential consequences, rewriting response headers can be a powerful solution to overcome issues. For instance, you can correct a server's misconfigured Cache-Control response header to improve response caching.

```kotlin
val rewriteCacheControlInterceptor = Interceptor { chain ->
    val originalResponse = chain.proceed(chain.request())
    val modifiedResponse = originalResponse.newBuilder()
        .header("Cache-Control", "max-age=60")
        .build()
    modifiedResponse
}
```

---

## conclusion

interceptors in OkHttp are powerful tools that enable developers to efficiently handle various tasks like logging, authentication, caching, and error handling in Android applications.

By understanding the working principles and types of interceptors, developers can enhance their applications' performance and functionality while maintaining a clean and modular codebase.