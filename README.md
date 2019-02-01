<p align="right"><sub><sup>Beware of the dancing Gandalf...</sub></sup></p>
<h1 align="center">🇺🇸🇺🇸 LOLzwagon 🇺🇸🇺🇸</h1>

<h4 align="center">Significantly bumps up your iOS XCTest code coverage and makes all unit tests pass... by crippling them</h4>

<p align="center">
  <img width="120" height="120" src="https://github.com/DerekSelander/LOLzwagon/raw/master/media/logo.png">
  <br />
  <i>"You know a repo is legit if it has a logo for it"</i>
</p>
Are you... 

* Looking to get a raise with the least amount of work possible?
* Having to deal with a superior and explain to them (on numerous occassions...) that it's extremely difficult (if not impossible) to get past 95% of code completion in your repo?
* In an office argument with the backened team and you want them to learn by example by not sucking and finally doing TDD?

<h4>IF YOU SAID "YES" TO ANY OF THE ABOVE, THIS REPO IS FOR YOU!</h4>

This code will neuter all `XCTAssert*`/`XCTestExpectation` functions/methods called on for testing. In addition, this dylib will greatly increase the code coverage of all modules which contain code coverage.

Check them pics out!

<p align="center">
  <img width="800" src="https://github.com/DerekSelander/LOLzwagon/raw/master/media/screen1.png">
</p>

<p align="center">
  <img width="800" src="https://github.com/DerekSelander/LOLzwagon/raw/master/media/screen2.png">
</p>

## Compiling

Download the Xcode project and build the **LOLzwagon Xcode scheme**. 

```
xcodebuild -project LOLzwagon.xcodeproj -scheme LOLzwagon -sdk iphonesimulator -config Debug
```

I specified using the **Debug** scheme, but feel free to also use the **Release** one. There's also the **GimmeARaise** scheme, but more on that in a sec...

After successfully compiling, the LOLzwagon will be placed at the following:

```
/usr/local/lib/libLOLzwagon.dylib
```

If you load this framework into your process, it will cripple Xcode's Unit Testing! 🎉 Check out the **Integratin** section for more info.


## Testing

Bundled into the Xcode project is a scheme called **CodeCoverage**. Run the unit tests and observe the `XCTest` scenarios. The logic in the tests should fail, but OMG, they'll pass!

```
xcodebuild test -project LOLzwagon.xcodeproj -scheme CodeCoverage -sdk iphonesimulator -config Debug
```

<!---
## Integrating

There are several ways to get this code to run on your 5-year-old CI/CD mac mini and loaded into test builds

Let's go through some of the ways that you can do this...

1. Just compile the `LOLzwagon.m` file into your application. This is definitely not recommended, since your `git`/`svn`/whatever credentials are tied to your action.
2. The second to worst idea is to use the **DYLD_INSERT_LIBRARIES** environment variable. This environment variable loads a framework into a process before anything else is loaded (while still honoring it's `LC_LOAD_DYLIB` dependencies first). Again, it's still tied to source control (especially if a shared Xcode scheme), so still not a good idea.

<p align="center">
  <img width="600" src="https://github.com/DerekSelander/LOLzwagon/raw/master/media/scheme.png">
</p>

3. A more subtle way is to use a launch daemon. Your Jenkins build machine will likely `git clone` your repo to a specific directory. You can use a `launchd` daemon to monitor the directory and perform an action if something changes.


## How Does it Work?

You probably don't care about this... 

––>

## Code Coverage

Building the `Debug` config will bump the unit tests up considerably in your application, but if you really, really want to shoot high for Code Coverage, you should compile your application with the **GimmeARaise** Xcode config

```
xcodebuild test -project LOLzwagon.xcodeproj -scheme CodeCoverage -sdk iphonesimulator -config GimmeARaise
```

Warning, this might make your Code Coverage a little too good. Might be better to make it slightly lower to glide under the radar. 

 <sub><sup>Also, don't use this in a production codebase... or any codebase </sub></sup>
