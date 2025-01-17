# Minecraft Authenticator

A minecraft authentication library that allows mojang ([yggdrasil](https://wiki.vg/Authentication)) and microsoft ([xbox live](https://wiki.vg/Microsoft_Authentication_Scheme)) accounts to be logged in and returns a minecraft profile with an access token.
This library also allows for storage of the authentication data and therefore sessions can be refreshed without a new login on the users side.

# Building

To build just run ``./gradlew build``. You will find the jars in the build/libs directory.
This project requires gson, guava and jopt-simple as dependencies.

# Include in your own project

To include this project you can use the maven build of this project which will resolve all required dependencies automatically.
The latest version is the latest tag in github.

```gradle
repositories {
	maven {
		url = "https://repo.u-team.info"
	}
}

dependencies {
	implementation "net.hycrafthd:minecraft_authenticator:XYZ"
}
```

# Usage

The main public facing api is the [Authenticator](src/main/java/net/hycrafthd/minecraft_authenticator/login/Authenticator.java) class. 
This class is documented and you should have a look here about more information. The following code snippets are just some simple usage demonstrations.

### Here is a simple login with yggdrasil

```java
try {
	final Authenticator authenticator = Authenticator.ofYggdrasil(clientToken, username, password).shouldAuthenticate().run();
	final AuthenticationFile file = authenticator.getResultFile();
	final Optional<User> user = authenticator.getUser();
	// write authentication file e.g. with file.write(path)
} catch (AuthenticationException ex) {
	// Handle exception
}
```

### Here is a simple login with microsoft

```java
try {
	final Authenticator authenticator = Authenticator.ofMicrosoft(authorizationCode).shouldAuthenticate().run();
	final AuthenticationFile file = authenticator.getResultFile();
	final Optional<User> user = authenticator.getUser();
	// write authentication file e.g. with file.write(path)
} catch (AuthenticationException ex) {
	// Handle exception
}
```

### Here is an login with an existing authentication file to refresh the session

```java
try {
	final Authenticator authenticator = Authenticator.of(authFile).shouldAuthenticate().run();
	final AuthenticationFile file = authenticator.getResultFile();
	final Optional<User> user = authenticator.getUser();
	// write authentication file e.g. with file.write(path)
} catch (AuthenticationException ex) {
	// Handle exception
}
```

# License

This project is licensed under apache 2 license. For more information see [here](LICENSE).
