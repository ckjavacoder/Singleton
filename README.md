
[![Raizlabs Repository](http://img.shields.io/badge/Raizlabs%20Repository-1.0.0-blue.svg?style=flat)](https://github.com/Raizlabs/maven-releases)
[![Android-Libs](https://img.shields.io/badge/Android--Libs-Singleton-orange.svg?style=flat)](http://android-libs.com/lib/singleton)

# Singleton

A very, very compact library that enables you to create __on-demand__ singletons within your application and easily store them to disk. Utilizing a dead-simple API, this library makes creating singletons and persisting data much more fun!

## Getting Started

Add the maven repo url to your build.gradle:

```groovy

  repositories {
        maven { url "https://raw.github.com/Raizlabs/maven-releases/master/releases" }
  }

```

Add the library to the project-level build.gradle, using the [apt plugin](https://bitbucket.org/hvisser/android-apt) and the 
[AARLinkSources](https://github.com/xujiaao/AARLinkSources) plugin::

```groovy

  dependencies {
    compile 'com.raizlabs.android:Singleton:1.0.0'
    aarLinkSources 'com.raizlabs.android:Singleton:1.0.0:sources@jar'
  }

```

## Usage

We want to use a Singleton. It should be easy, statically referenced, and **only** created when we need it (lazy instantiation).

### Using the Singleton Class

#### Configuration

In your ```Application``` class, call:

```java
 
  Singleton.init(this);

```

#### Retrieval

Features:
  1. Will create a singleton for you using the default constructor of the object if it does not exist already. 
  2. **Tagging**: enables multiple different singletons in memory or on disk that belong to the same class.
  3. Disk objects must be serializable
  4. On-demand memory usage so you can release an object onto disk and retrieve it when you need it!

```java

public void someMethod() {
  
  // Retrieves the singleton instance into a local variable!
  MyClass myObject = new Singleton(MyClass.class).getInstance();

  // Retrieve with a tag
  MyClass myObject = new Singleton("Tag", MyClass.class).getInstance();
  
}

```

#### Removal

Use the singleton to free up or delete memory.

```java

  // Deletes from persistent storage if saved, and released from the map and current singleton referent
  mySingleton.delete();

  // Removes the grasp on the contained reference and sets it to null. 
  // Good for freeing up persistent data
  mySingleton.release();

```

#### Storing

Will automatically convert the ```Singleton``` to persistent as long as it's ```Serializable```, otherwise an exception will be logged.

```java
  
   // Saves the object to persistent storage
   mySingleton.save();

```
