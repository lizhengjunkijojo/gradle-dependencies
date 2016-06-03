# gradle-dependencies
# 一、Android studio 中配置使用jCenter和Maven Central仓库
仓库的依赖
依赖包的定义格式
仓库的导入和维护
一、仓库的依赖使用
在项目app目录下的build.gradle 中添加依赖使用：
dependencies {
    compile 'com.loopj.android:android-async-http:1.4.9'
}
二、依赖包的定义格式
com.loopj.android:android-async-http:1.4.9
GROUP_ID 组名 com.loopj.android
ARTIFACT_ID 真实名 android-async-http
VERSION 版本号  1.4.9
三、jCenter和Maven Central仓库，配置导入格式
在项目目录下的build.gradle 中添加依赖导入：
1.jCenter是由bintray.com进行维护的Maven仓库
导入格式
allprojects {
    repositories {
        jcenter()
    }
}

2.Maven Central是由sonatype.org进行维护的Maven仓库
allprojects {
    repositories {
        mavenCentral()
    }
}

# 二、Mac 中Sndroid Studio中配置使用自定义仓库JitPack.io
Android  Studio 中使用Gradle依赖有一下三种方式：
jCenter中央仓库
Maven Central中央仓库
使用其他自定义的仓库，例：JitPack.io  Fabric.io等


一、仓库简介
仓库一般需要三步骤:
1.	仓库中依赖包发布
2.	仓库在代码中导入
3.	仓库依赖包中项目中引用
二、jcenter和maven central的一般流程：
发布： 注册 ，登录， 配置参数，Build ，Push，等待验证，通过
三、jitpack.io代替jcenter发布github项目：
步骤：jitpack是一个自定义的Maven仓库
1.在jitpack网站，输入Github项目地址，点Look up    发布
2.配置自定义仓库
allprojects {
    repositories {
        。。。
        maven{url “https://jitpack.io”}
    }
}
3. 加入依赖
dependencies {
    compile('com.github.afollestad.material-dialogs:core:0.8.5.3@aar') {
    transitive = true}
}

四、Twitter的Fabric.io
maven {   url ‘https://maven.fabric.io/public’  } 




# 三、整体使用：
1.项目下的build.gradle文件中：
buildscript {
    repositories {
        jcenter()
    }
    dependencies{
        classpath 'com.android.tools.build:gradle:2.1.0'
    }
}

allprojects {
    repositories {
        jcenter()
        mavenCentral()
        maven { url "https://raw.githubusercontent.com/umeng/mvn-repo-umeng/master/repository" }
        maven { url "https://jitpack.io" }
    }
}

2．项目app下的build.gradle文件中：
apply plugin: 'com.android.library'

android {
    compileSdkVersion 23
    buildToolsVersion '21.0.1'
    useLibrary 'org.apache.http.legacy'
    defaultConfig {
        minSdkVersion 10
        targetSdkVersion 23
        versionCode 1
        versionName "1.0"
    }
    buildTypes {
        release {
            minifyEnabled false
            shrinkResources true
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
    sourceSets {
        main {
            jniLibs.srcDirs = ['libs']
        }
    }
}

dependencies {
    compile fileTree(include: ['*.jar'], dir: 'libs')
    compile 'com.android.support:appcompat-v7:23.1.1'
    compile 'me.gujun.android.taggroup:library:1.4@aar'
    compile 'com.nineoldandroids:library:2.4.0'
    compile('com.github.afollestad.material-dialogs:core:0.8.5.3@aar') {
        transitive = true
    }
    compile 'de.greenrobot:eventbus:2.4.0'
    compile 'com.squareup.okhttp:okhttp:2.4.0'
}
