[![](https://jitpack.io/v/anyms/fetcher.svg)](https://jitpack.io/#anyms/fetcher)
[![Build Status](https://travis-ci.org/anyms/fetcher.svg?branch=master)](https://travis-ci.org/anyms/fetcher)
[![License](https://img.shields.io/github/license/anyms/fetcher.svg)](https://github.com/anyms/fetcher/blob/master/LICENSE)

# Fetcher - A Human Friendly HTTP Library for Android


Android apps created using Fetcher.

[<img src="https://i.ibb.co/y88vTtp/web-hi-res-512.png" alt="Get it on Google Play" height="100">](https://play.google.com/store/apps/details?id=app.spidy.fetcher)
[<img src="https://play.google.com/intl/en_us/badges/images/generic/en_badge_web_generic.png" alt="Get it on Google Play" height="80">](https://play.google.com/store/apps/details?id=app.spidy.fetcher)

> Fetcher is for human by human.

![image](https://i.ibb.co/tpB7DqP/black-german-shepherd-d-4.jpg)

# Getting Started

Add it in your root build.gradle at the end of repositories

```css
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}
```

Add the dependency

```css
dependencies {
        implementation 'com.github.anyms:fetcher:Tag'
}
```

# Using it so Simple.

Create a fetcher instance.

```kotlin
val fetcher = Fetcher()
```

Now you are ready to see the power of fetcher.

```kotlin
// simple GET request
fetcher.get("http://httpbin.org/get")
    .ifSucceed { response -> }
    .ifFailed { response -> }

// simple POST request
fetcher.post("http://httpbin.org/post")
    .ifSucceed { response -> }
    .ifFailed { response -> }

// sending parameters with your request
val params = hashMapOf(
    "name" to "Fetcher",
    "age" to 1
)
fetcher.get("http://httpbin.org/get", params = params)
    .ifSucceed { response -> }
    .ifFailed { response -> }
```

Download binary files

```kotlin
fetcher.get("http://httpbin.org/get", isStream = true)
    .ifSucceed { response -> }
    .ifFailed { response -> }
    .ifStream { bytes ->
        if (bytes != null) {
            // writing bytes to a file
            ...
        } else {
            // closing the opened file
            ...
        }
    }
```


### Classic requests

Classic requests doesn't have any callbacks, which means it returns the response, you have to run classic methods in a thread.

To use classic methods, you need to create a new instance from Fetcher

```kotlin
val fetcher = Fetcher().Classic()
```

Use case:

```kotlin
// simple GET request
val response = fetcher.get("http://httpbin.org/get")

// simple POST request
val response = fetcher.post("http://httpbin.org/post")

// sending parameters with your request
val params = hashMapOf(
    "name" to "Fetcher",
    "age" to 1
)
val response = fetcher.get("http://httpbin.org/get", params = params)
```


