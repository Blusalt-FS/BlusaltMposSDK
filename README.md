# HorizonPosSDK

## Installation

## Step 1
```sh
#Create a github.properties file in the root folder of android. Path should be like below: E.g. "mySampleApp/android/github.properties"

# Add the following in github.properties:
USERNAME_GITHUB=MyUsernameOnGithub
TOKEN_GITHUB=TokenFromGithubClassicToken
```

## Step 2: build.gradle (project level)
Add the following to build.gradle(project level) file
```sh


buildscript {
    repositories {
      ...
    }
    dependencies {
      ...
    }
}

allprojects {
    def githubPropertiesFile = rootProject.file("github.properties")
    def githubProperties = new Properties()
    githubProperties.load(new FileInputStream(githubPropertiesFile))

    repositories {
        ...
                
        maven {
          url 'https://gitlab.com/api/v4/projects/4128550/packages/maven'
        }
        maven {
          name "GitHubPackages"
          url 'https://maven.pkg.github.com/Blusalt-FS/BlusaltMposSDK'

          credentials {
            username githubProperties['USERNAME_GITHUB']
              password githubProperties['TOKEN_GITHUB']
            }
       }
    }
}

```


## Step 3: build.gradle (app)
All the following to build.gradle (app level)

```sh

dependencies{
  implementation 'net.blusalt:blusaltmpos:1.0'
}
```


## Usage

## Kotlin
```kt




class MainActivity : AppActivityCompact {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main_pos)
        Pos.getINSTANCE().startMPOSplugin(this, "", object : TransactionCompletedCallBack {
            override fun onSuccess(terminalResponse: TerminalResponse?) {

            }

            override fun onFailure(statusCode: Int, errorObject: String?) {

            }


        })
    }
}
```

## Java
```java
class MainActivity extends AppActivityCompact {
    @override
    void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main_pos);

        Pos.getINSTANCE().startMPOSplugin(this, "", new TransactionCompletedCallBack() {
            @Override
            public void onSuccess(TerminalResponse terminalResponse) {

            }

            @Override
            public void onFailure(int statusCode, String errorObject) {

            }
        });
    }
}



