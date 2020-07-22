# opencv-android

OpenCV4Android, packaged as a .aar for direct use without depending on the stupid OpenCV Manager app.

### Credit:

This is a fork from [steveliles/opencv-android](https://github.com/steveliles/opencv-android) project, changes was made to allow building on jitpack.io service.

### Using your glorious new .aar

Reference the maven repository you've deployed your .aar to, e.g. mine (which I can't stop you from using ;)) is:

    allprojects {
      repositories {
        jcenter()
        maven { url "https://jitpack.io" }
      }
    }

Include the .aar in your build.gradle file:

    dependencies {
        implementation 'com.github.ctodobom:opencv-android:3.1.0'
    }

**Attention:** Be sure to check if the referenced version is the one you want, and if it available on the [Releases Section](https://github.com/ctodobom/opencv-android/releases) of this project. You can always use a commit hash or `-SNAPSHOT` (not recommended) as the version number.

Bootstrap OpenCV in your Java code:
    
    import org.opencv.android.OpenCVLoader;
    
    ...
    
    if (OpenCVLoader.initDebug()) {
      // do some opencv stuff
    }

Optional but recommended: to keep the downloaded APK size to a minimum, build separate APK's per architecture (approx 10MB each vs 42MB for universal) by placing the following inside the 'android' gradle directive of your application's build.gradle:

    splits {
      abi {
        enable true
        reset()
        include 'x86', 'x86_64', 'armeabi', 'armeabi-v7a', 'mips', 'mips64', 'arm64-v8a'
        universalApk false
      }
    }


### Building an .aar of OpenCV-3.x.y for yourself

This instructions are from original author [@steveliles](https://github.com/steveliles) - will be tested and updated when upgrading to newer version of OpenCV.

Building OpenCV-3.x.y for Android is actually quite simple, its just not obvious where to get the pieces and the OpenCV docs hard-sell the "OpenCV Manager" in favour of the better and easier direct integration approach.

Here's the steps I used to create my .aar:

1. Download and extract the OpenCV4Android bundle
2. Create a Library Project in Android Studio
3. Copy the java source files from OpenCV4Android into src/main/java
4. Drop the OpenCV native libraries into src/main/jniLibs
5. Run the gradle build
6. Et voila, .aar file

### Disclaimer

This project is simply my bundling of OpenCV as an Android Library. I am not otherwise involved in the OpenCV project, and all credit for the wonderful OpenCV library goes to the developers thereof.
