# AntiFraud SDK Publisher
This is demo app to show usage of AntiFraud SDK 


## Installation
Here are the steps to install sdk to new Host project:
1. Open / Create local.properties of Host project
2. Copy & paste following credential: `gpr.key=glpat--qZJsybnvhRJExJnZPBS`
3. Open Host project settings.gradle
4. Copy & Paste to top of file
```
val githubProperties =  Properties()
githubProperties.load( FileInputStream("${rootProject.projectDir}/local.properties"))
val projectID="3"
```

5. Copy & paste following config details to repository block :
```
 maven {
            name = "GitLab"
            url = uri("https://git.rtmc.uz/api/v4/projects/$projectID/packages/maven")
            credentials(HttpHeaderCredentials::class) {
                name = "Private-Token"
                value = (githubProperties["gpr.key"] ?: "NO_TOKEN") as String?
            }
            authentication {
                create<HttpHeaderAuthentication>("header")
            }
        }
        
```

6. Open Host project's  build.gradle file in app level
7. Add `implementation ("uz.tbm.antifraud:sdk-test:1.1.1")` to dependencies block
8. Sync Host Project. After successful syncronization, AntiFraud SDK is ready to use.

## Usage
Here is basic information about  AntiFraud SDK's method:

```
// SDK instance
AntiFraudLibrary("http://agent.host.ip.address:port",context, contentResolver)


// SDK Init
fun initialize(
        configuration: AntiFraudConfiguration,
        onResult: (Result<Unit>) -> Unit
    )
data class AntiFraudConfiguration(
    val tokenType: String,
    val accessToken: String
)

// SMS Code Verification
fun verifySmsCode(phoneNumber: String, code: String, onResult: (Result<Unit>) -> Unit)


// Open face detector page
showFace(faceConfiguration, faceCompletion = faceCompletion)

data class AFFaceConfiguration(
    val context: Context,
    val document: String?,
    val birthDate: String?
)
val faceCompletion= object : AFFaceCompletion {
    override fun onComplete(success: Boolean, error: Throwable?) {
        if (success){
            // Success case
        } else {
            //Error case - error message defines the reason
        }
    }
}

// Authenticate via Face
fun faceAuth(
        photoBase64: String,
        document: String?,
        birthDate: String?
    ): Result<Unit> 


// Face Auth Confirmation  
fun confirmFace(
        document: String,
        birthDate: String
    ): Result<Unit> 

    
// Gather information and Send them to Backend to check Fraud on device
 fun detectFraud(code: String, onResult: (Result<Unit>) -> Unit)

    
// Refresh Token   
fun refreshToken(token: String): Result<Unit>
    
    
 // Logout from system
fun logout(): Result<Unit>
```

For more usage details and method explanation, please refer to **AntiFraud SDK Publisher App** or **Documentation** that will be provided once NDA is signed. 


## Support
Please reach out subscontrol.dev@gmail.com for any help, regarding to Integration, SDK Usage etc.


## License
@All Rights Reserved - TBM UZ Android SDK 2024. 

TBM UZ Android SDK is proprietary software developed by TBM UZ. By using this SDK, you agree to abide by the terms and conditions set forth in the license agreement provided by TBM UZ.

Unauthorized reproduction, distribution, or modification of this SDK or any part thereof is strictly prohibited. This SDK is provided "as is," without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and non-infringement.

For more information about licensing and usage rights, please contact TBM UZ at subscontrol.dev@gmail.com.

