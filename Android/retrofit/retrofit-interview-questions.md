# 🔌 Retrofit Android Interview Q&A Guide

A complete guide to understanding **Retrofit**, one of the most powerful HTTP clients for Android used for network communication and REST API integration.

---

## 1. What is Retrofit?

**Retrofit** is a type-safe HTTP client developed by **Square** for Android and Java, used to simplify network requests to REST APIs. It uses annotations to define how HTTP requests are made and handles JSON conversion using converter libraries.

---

## 2. Advantages of Retrofit

- Type-safe REST client
- Easy to implement and read
- Supports various converters (Gson, Moshi, etc.)
- Supports synchronous and asynchronous calls
- Built-in support for headers, query/path/body parameters
- Easily extendable via interceptors and custom clients

---

## 3. What is @GET, @POST, @PUT, @DELETE?

Retrofit uses annotations to specify HTTP methods:

```kotlin
@GET("users")
@POST("users")
@PUT("users/{id}")
@DELETE("users/{id}")
```

## 4. How to Create a Retrofit Builder Instance?
```kotlin
val retrofit = Retrofit.Builder()
    .baseUrl("https://api.example.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .build()
```

## 5. How to Create Service Interface Methods?
```kotlin
interface ApiService {
    @GET("users")
    fun getUsers(): Call<List<User>>

    @POST("users")
    fun createUser(@Body user: User): Call<User>
}
```

## 6. How to Consume API Using Interface Methods?
```kotlin
val api = retrofit.create(ApiService::class.java)

api.getUsers().enqueue(object : Callback<List<User>> {
    override fun onResponse(call: Call<List<User>>, response: Response<List<User>>) {
        // Handle response
    }

    override fun onFailure(call: Call<List<User>>, t: Throwable) {
        // Handle error
    }
})
```
## 7. What is converterFactory in Retrofit Builder?
It defines how Retrofit converts the response and request body.

Examples:

```kotlin
GsonConverterFactory.create()
MoshiConverterFactory.create()
ScalarsConverterFactory.create()
```

## 8. Difference Between enqueue and execute

| Method    | Description                      | Thread                     |
| --------- | -------------------------------- | -------------------------- |
| `enqueue` | Asynchronous, runs on background | Yes                        |
| `execute` | Synchronous, runs on main thread | No (not recommended on UI) |

## 9. What is @Header?
Used to send custom headers with requests.
```kotlin
@GET("users")
fun getUsers(@Header("Authorization") token: String): Call<List<User>>
```

## 10. How to Pass Static Headers?
```kotlin
@Headers("Content-Type: application/json", "Cache-Control: no-cache")
@GET("users")
fun getUsers(): Call<List<User>>
```

## 11. How to Pass Dynamic Headers?
```kotlin
@GET("users")
fun getUsers(@Header("Authorization") token: String): Call<List<User>>
```

## 12. How to Send JSON Requests?
```kotlin
@POST("users")
fun sendUser(@Body user: User): Call<User>
```

## 13. How to Send Requests with Query Parameters?
```kotlin
@GET("users")
fun getUsers(@Query("page") page: Int): Call<List<User>>
```

## 14. How to Send Requests with Path Parameters?
```kotlin
@GET("users/{id}")
fun getUser(@Path("id") id: Int): Call<User>
```

## 15. How to Implement File Uploads Using Retrofit?
```kotlin
@Multipart
@POST("upload")
fun uploadFile(@Part file: MultipartBody.Part): Call<ResponseBody>
```

Creating MultipartBody.Part:

```kotlin
val file = File("path_to_file")
val requestFile = file.asRequestBody("image/*".toMediaTypeOrNull())
val body = MultipartBody.Part.createFormData("file", file.name, requestFile)
```

## 16. How to Cancel an Ongoing Request?
```kotlin
val call = api.getUsers()
call.cancel()
```

## 17. How to Change Timeouts (Connect, Read, Write)?
```kotlin
val client = OkHttpClient.Builder()
    .connectTimeout(30, TimeUnit.SECONDS)
    .readTimeout(30, TimeUnit.SECONDS)
    .writeTimeout(30, TimeUnit.SECONDS)
    .build()

val retrofit = Retrofit.Builder()
    .baseUrl("https://api.example.com/")
    .client(client)
    .addConverterFactory(GsonConverterFactory.create())
    .build()
```

## 18. What is an Interceptor?
Interceptors allow you to inspect, modify, or retry requests/responses.
```kotlin
val interceptor = Interceptor { chain ->
    val request = chain.request().newBuilder()
        .addHeader("Authorization", "Bearer TOKEN")
        .build()
    chain.proceed(request)
}
```
Add to client:

```kotlin
val client = OkHttpClient.Builder()
    .addInterceptor(interceptor)
    .build()
```
## 19. Scenarios Where Interceptors Are Used
Logging API requests/responses

- Adding headers (auth tokens, content types)
- Handling errors globally
- Retrying failed requests
- Encrypting/decrypting data

## 20. Retrofit Retry Policy
```kotlin
Retrofit doesn’t provide a retry policy like Volley, but it can be implemented manually:
class RetryInterceptor(private val maxRetries: Int) : Interceptor {
    override fun intercept(chain: Interceptor.Chain): Response {
        var request = chain.request()
        var response: Response
        var retryCount = 0
        do {
            response = chain.proceed(request)
            retryCount++
        } while (!response.isSuccessful && retryCount < maxRetries)
        return response
    }
}
```

## 21. How to Cache Response Data (Offline Support)?
```kotlin
val cache = Cache(File(context.cacheDir, "http_cache"), 10 * 1024 * 1024)

val client = OkHttpClient.Builder()
    .cache(cache)
    .addInterceptor { chain ->
        var request = chain.request()
        if (!isNetworkAvailable()) {
            request = request.newBuilder()
                .header("Cache-Control", "public, only-if-cached, max-stale=2419200")
                .build()
        }
        chain.proceed(request)
    }
    .build()
```

## 22. REST API Security in Retrofit
- Use HTTPS (SSL/TLS)
- Add Authorization headers (Token/Bearer)
- Use Interceptors to add auth headers
- Validate server certificates (SSL Pinning)
- Avoid exposing sensitive data in logs

## 23. What is SSL Pinning in Retrofit?
```kotlin
SSL Pinning protects against man-in-the-middle (MITM) attacks by validating the server's certificate.
val certificatePinner = CertificatePinner.Builder()
    .add("api.example.com", "sha256/xxxxxxxxxx")
    .build()

val client = OkHttpClient.Builder()
    .certificatePinner(certificatePinner)
    .build()
```

## 24. How to Troubleshoot Retrofit Requests?
Use HttpLoggingInterceptor for full logs:
```kotlin
val logging = HttpLoggingInterceptor().apply {
    level = HttpLoggingInterceptor.Level.BODY
}
```
Check:
- Internet permissions
- Base URL
- Serialization errors
- HTTP response codes
- Network availability








