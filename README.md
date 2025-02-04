# ezyfox-server <img src="https://github.com/youngmonkeys/ezyfox-server/blob/master/logo.png" width="64" />

[![Build Status](https://travis-ci.org/youngmonkeys/ezyfox-server.svg?branch=master)](https://travis-ci.org/youngmonkeys/ezyfox-server)

# Documentation

1. [https://youngmonkeys.org/get-started/](https://youngmonkeys.org/get-started/)

2. [https://youngmonkeys.org/ezyfox-sever/](https://youngmonkeys.org/project/ezyfox-sever/)

# Synopsis

Ezyfox Server is a socket server. It supports TCP, UDP and Websocket protocol. It also provides manipulation beans, auto binding, auto implementation and more utilities.

# Dependency

```xml
<dependency>
    <groupId>com.tvd12</groupId>
    <artifactId>ezyfox-server-embedded</artifactId>
    <version>1.1.9</version>
</dependency>
```

# Benchmark

Ezyfox Server's benchmark with 1000 CCU broadcast messages in 1 hour on one VPS ram 512MB, CPU 1 core

<img src="https://github.com/youngmonkeys/ezyfox-server/blob/master/images/ezyfox_1h.png" width="747" height="320" />

# Code Example

**1. Create an app entry**

```java
public static class HelloAppEntry extends EzySimpleAppEntry {

    @Override
    protected String[] getScanableBeanPackages() {
        return new String[] {
                "com.tvd12.ezyfoxserver.embedded.test" // replace by your package
        };
    }

    @Override
    protected String[] getScanableBindingPackages() {
        return new String[] {
                "com.tvd12.ezyfoxserver.embedded.test" // replace by your package
        };
    }
    
    @Override
    protected EzyAppRequestController newUserRequestController(EzyBeanContext beanContext) {
        return EzyUserRequestAppSingletonController.builder()
                .beanContext(beanContext)
                .build();
    }
    
}
```

**2. Create a plugin entry**

```java
public static class HelloPluginEntry extends EzySimplePluginEntry {

    @Override
    protected String[] getScanableBeanPackages() {
        return new String[] {
                "com.tvd12.ezyfoxserver.embedded.test" // replace by your package
        };
    }

}
```

**3. Setup**

```java
EzyPluginSettingBuilder pluginSettingBuilder = new EzyPluginSettingBuilder()
        .name("hello")
        .addListenEvent(EzyEventType.USER_LOGIN)
        .entryLoader(HelloPluginEntryLoader.class);

EzyAppSettingBuilder appSettingBuilder = new EzyAppSettingBuilder()
        .name("hello")
        .entryLoader(HelloAppEntryLoader.class);

EzyZoneSettingBuilder zoneSettingBuilder = new EzyZoneSettingBuilder()
        .name("hello")
        .application(appSettingBuilder.build())
        .plugin(pluginSettingBuilder.build());

EzySimpleSettings settings = new EzySettingsBuilder()
        .zone(zoneSettingBuilder.build())
        .build();
```

**4. Create and start a server**

```java
EzyEmbeddedServer server = EzyEmbeddedServer.builder()
        .settings(settings)
        .build();
server.start();
```

You can find full example [here](https://youngmonkeys.org/use-embedded-server/)

# Used by

1. [Free Chat](https://youngmonkeys.org/asset/freechat/)
2. [Space Game Cocos2d-x](https://youngmonkeys.org/asset/space-game/)
3. [Space Shooter Unity](https://youngmonkeys.org/asset/space-shooter/)
4. [Lucky Wheel Phaser HTML5](https://youngmonkeys.org/asset/lucky-wheel/)

# Motivation

We are game server developers, We have a lot of online games and We must buy game server engine like SmarfoxServer
or Photon but they are really expensive. We need make a change to help us and everyone. 
Free is good idea and We make Ezyfox server

# API Reference

# Tests

mvn test

# Contributors

 - [DungTV](mailto:itprono3@gmail.com)

# License

- Apache License, Version 2.0
