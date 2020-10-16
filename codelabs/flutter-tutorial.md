author: Drăghici Marius-Robert
title: Flutter tutorial
summary: A step by step tutorial for creating Flutter applications.
id: flutter-tutorial
categories: web
environments: Flutter
status: draft
feedback link: https://github.com/robert-marius-draghici/my-codelabs/issues

# Flutter tutorial

## What is Flutter?
Duration: 1

Flutter is a free and open-source, cross-platform development framework created by Google. 
It is used to develop high-performance, native mobile applications for iOS and Android from a single code base.
Apart from mobile platforms, it can also be used to develop applications for Windows, Mac, Linux, Google Fuchsia OS and the web.

## Why Flutter?
Duration: 5

There are three ways to develop applications for mobile:
- native means that we use the native, official tools such as Android Studio with Java and Kotlin for Android or Xcode with Swift and Objective-C for iOS. Even though we can build fast and reliable apps with these tools, the disadvantage is that we need to write the application for each platform.
- hybrid (such as Xamarin, Ionic, React Native) provides a bridge between the code and the mobile operating system so that the same code can be used on any mobile platform. However, this can cause performance and integration issues.
- web means that the application is written in HTML, CSS, Javascript and can be accessed through a browser. We only need one codebase for any system. The disadvantage is that the application cannot access the more advanced features of the device and the application is just a website in the form of an app.

### How does Flutter overcome this issues?
Flutter falls in the hybrid category and was developed by Google with features that overcome the current issues with hybrid apps:
- Flutter compiles to native for excellent performance. It supports Just in Time Compilation (code is recompiled in real time allowing for hot reload) and Ahead of Time Compilation (code is compiled to native ARM code for great performance on any device).
- Fast development.
- Great user experience.
- Single code base for multiple platforms (Android, iOS, web, Windows etc).
- It does not have bridges between the code and the device.

## The Dart language
Duration: 1

Flutter applications are written in Dart which is a programming language developed by Google. Dart is an object-oriented language that supports both ahead-of-time and just-in-time compilation. The Dart language offers many of the features seen in other languages including garbage collection, async-await, strong typing, generics, as well as a rich standard library.

## Create a Hello World project in Flutter.
Duration: 10

Follow the instructions from [here](https://flutter.dev/docs/get-started/test-drive?tab=androidstudio#androidstudio) in order to create a new application, which will be named hello_flutter.

Remove the widget_test.dart file as it will not be required for the moment.
Remove the starting code from main.dart and replace with the following:

```dart
import 'package:flutter/material.dart'; // #1

void main() { // #2
  runApp( // #3
    Center( // #4
      child: Text( // #5
        "Hello, Flutter!",
        textDirection: TextDirection.ltr // #6
      ),
    )
  );
}
```

1. This package contains Widgets that implement Material design, a design language developed by Google. A package is simply a library of functions.
2. The main method is the entry point of a Flutter app.
3. The runApp method inflates a Widget and attaches it to the screen. In other words, it will show on the screen the Widget passed to this method.
4. Everything in Flutter is a Widget so Center and Text are Widgets. The new keyword is not needed anymore in later versions of Flutter. Center is a container Widget that centers its content onto the screen both horizontally and vertically.
5. The child property allows us to nest Widgets inside other Widgets. Text is just a text box.
6. The Text Widget requires that a text direction is specified.

## Enhance the design of the Flutter App.
Duration: 10

In order to enhance the design of the application, we can use a MaterialApp Widget to wrap the other widgets. The MaterialApp Widget is an application that uses material design and wraps a number of widgets that are commonly required for material design applications. The MaterialApp allows us to customize our application with its properties.

Modify the code as follows:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp( // #1
      title: "Hello Flutter App", // #2 
      home: Material( // #3
        color: Colors.teal, #4
        child: Center( #5
          child: Text(
            "Hello, Flutter!",
            textDirection: TextDirection.ltr, 
            style: TextStyle(color: Colors.white, fontSize: 36.0), #6
          ),
        ),
      )));
}
```

1. The MaterialApp Widget is usually the container of the other widgets in our application. It allows us to customize our application by adding a title, background color and others. It can also be useful for navigation and routing.
2. The title of the application. This is the title that the operating system will see.
3. The home property is the widget for the default route of the app. This is the route that is displayed first when the application is started normally, unless initialRoute is specified.
4. The Material class allows us to specify the color of its content (the background color in our example). Other properties are: shape, shadow, elevation and other properties that change the way it behaves.
5. Previously the Center Widget was passed directly to the runApp method. However, in Flutter Widgets can be nested using the child property.
6. Specify some style properties for the text. The fontSize requires a double. 

### Adding an application bar

The next step is to add an application bar. This is done by using the Scaffold Widget. The Scaffold class implements the basic material design visual layout structure. It provides APIs for showing drawers, snack bars and bottom sheets among others.

Modify the code to look like this:
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
      title: "Hello Flutter App", 
      home: Scaffold( // #1
          appBar: AppBar(title: Text("Title in App Bar")), // #2
          body: Material( // #3
            color: Colors.teal,
            child: Center(
              child: Text(
                "Hello, Flutter!",
                textDirection: TextDirection.ltr, 
                style: TextStyle(color: Colors.white, fontSize: 36.0),
              ),
            ),
          ))));
}
```

1. The Scaffold allows us to customize the layout of the application. 
2. The application bar.
3. The body represents the main content of the screen.

## Code organization for a Flutter application.
Duration: 10

Even though we can write the entire application code in the runApp method, this is not recommended especially if the application grows over time. In general, the main method should be as simple as possible.

The Flutter framework is written in the Dart programming language, which is an object-oriented language. This means that a Widget is nothing more than an object, an instance of a class. Although the Flutter framework provides many Widgets, we can also create our own. 

In order to simplify the main method, we will create a new class called HelloFlutterApp and move the application code in this class. The HelloFlutterApp class will extend the StatelessWidget abstract class, which is a generic Widget that does not have any state. Then, the HelloFlutterApp class needs to override the build method of the superclass. We move the MaterialApp Widget from main to the build method and in the runApp method we return a new instance of HelloFlutterApp. Also, we can further simplify the main method by using the arrow notation.

The code should look like this:
```dart
import 'package:flutter/material.dart';

void main() => runApp(new HelloFlutterApp()); // #1

class HelloFlutterApp extends StatelessWidget { // #2
  @override
  Widget build(BuildContext context) { // #3
    return MaterialApp(
        title: "Hello Flutter App",
        home: Scaffold(
            appBar: AppBar(title: Text("Title in App Bar")),
            body: Material(
              color: Colors.teal,
              child: Center(
                child: Text(
                  "Hello, Flutter!",
                  textDirection: TextDirection.ltr,
                  style: TextStyle(color: Colors.white, fontSize: 36.0),
                ),
              ),
            )));
  }
}
```

1. The main method now has only one line using the arrow notation. The application code was moved from the runApp method in the build method of HelloFlutterApp.
2. The class holding the definition of our application.
3. The build method inherited from StatelessWidget needs to be implemented, because it is an abstract method.

To further modularize the code, we can create a file for each class and files could be structured in packages such as screens, pages etc. For our application, we want to have the home screen (the material Widget in the home property)in a separate file. 

Create a new folder called screens in the lib directory. Then create a file home.dart and a class Home and move the code from the body property in the build method of the Home class.

The home.dart file should look like this:
```dart
import 'package:flutter/material.dart';

class Home extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Material(
      color: Colors.teal,
      child: Center(
        child: Text(
          "Hello, Flutter!",
          textDirection: TextDirection.ltr,
          style: TextStyle(color: Colors.white, fontSize: 36.0),
        ),
      ),
    );
  }
}
```

The main class will look like this:
```dart
import 'package:flutter/material.dart';

import 'screens/home.dart'; // #1

void main() => runApp(new HelloFlutterApp());

class HelloFlutterApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
        debugShowCheckedModeBanner: false, // #2
        title: "Hello Flutter App",
        home: Scaffold(
            appBar: AppBar(title: Text("Title in App Bar")), body: Home())); // #3
  }
}
```

1. Import the contents of the home.dart file.
2. debugShowCheckedModeBanner will remove the debug banner that appears in the top right corner of the app.
3. Replace the code from the body property with the class.

## Adding logic to a Flutter application.
Duration: 10

Since Widgets are instances of a class, we can add our own methods to a class to perform the business logic.

For our application, we want to customize the text shown in the Home screen. For this, we create a new method in the Home class called sayHello which returns a String.

Dart is a strongly typed language meaning that if we declare a variable of type String (String hello; for instance) then we cannot change its type later in the code. However, if we declare hello using var (var hello;) then hello can hold any type. It is recommended to specify the specific type for a variable and not use var. Numbers can be of type int, double and num (num can be either an int or a double).

Now we want our application to show a different text to the user based on the time of the day:
- before 12: "Good morning!"
- between 12-18: "Good afternoon!"
- after 18: "Good evening!"
Also, we want to show the current time.

The home.dart file should look like this:
```dart
import 'package:flutter/material.dart';

class Home extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Material(
      color: Colors.teal,
      child: Center(
        child: Text(
          sayHello(), // #1
          textDirection: TextDirection.ltr,
          style: TextStyle(color: Colors.white, fontSize: 36.0),
        ),
      ),
    );
  }

  String sayHello() {
    String hello;
    DateTime now = DateTime.now();
    int hour = now.hour;
    int minute = now.minute;
    String minutes = (minute < 10) ? "0" + minute.toString() : minute.toString(); // #2

    if (hour < 12) {
      hello = "Good morning!";
    } else if (hour < 18) {
      hello = "Good afternoon!";
    } else {
      hello = "Good evening!";
    }

    return "It's now " + hour.toString() + ":" + minutes + ".\n" + hello;
  }
}
```

1. Replace the hard-coded String with the one returned by the sayHello method.
2. We want the minutes to be shown in two digits.
