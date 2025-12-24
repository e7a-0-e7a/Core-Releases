# Core API - Release Repository

This repository contains the compiled releases of the Core API plugin for Minecraft servers.

## What is this repository?

This is a **public release repository** that contains only the built JAR files and Maven metadata. The source code is maintained in a separate private repository.

## Installation

### As a Plugin

1. Download the latest `Core-{VERSION}.jar` from the [Releases](https://github.com/e7a-0-e7a/Core-Releases/releases) page
2. Place it in your server's `plugins/` folder
3. Restart your server or use `/reload`

### As a Maven Dependency

Add this repository and dependency to your `pom.xml`:

```xml
<repositories>
    <repository>
        <id>core-releases</id>
        <url>https://raw.githubusercontent.com/e7a-0-e7a/Core-Releases/main</url>
    </repository>
    <repository>
        <id>spigotmc-repo</id>
        <url>https://hub.spigotmc.org/nexus/content/repositories/snapshots/</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>xyz.rhaven</groupId>
        <artifactId>Core</artifactId>
        <version>1.0.0</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
```

## Available Versions

All released versions are available in the Maven repository structure:
- `xyz/rhaven/Core/{VERSION}/Core-{VERSION}.jar`
- `xyz/rhaven/Core/{VERSION}/Core-{VERSION}.pom`

Check the [Releases](https://github.com/e7a-0-e7a/Core-Releases/releases) page for the latest version.

## Maven Repository Structure

```
xyz/
└── rhaven/
    └── Core/
        ├── maven-metadata.xml
        └── {VERSION}/
            ├── Core-{VERSION}.jar
            ├── Core-{VERSION}.pom
            ├── Core-{VERSION}.jar.sha1
            └── Core-{VERSION}.pom.sha1
```

## Usage in Your Plugin

Once you've added Core as a dependency, you can use it in your plugin:

```java
import xyz.rhaven.core.Core;
import xyz.rhaven.core.apis.*;

public class MyPlugin extends JavaPlugin {
    private Core core;
    
    @Override
    public void onEnable() {
        // Get Core instance
        Plugin corePlugin = getServer().getPluginManager().getPlugin("Core");
        if (corePlugin == null || !(corePlugin instanceof Core)) {
            getLogger().severe("Core plugin not found!");
            getServer().getPluginManager().disablePlugin(this);
            return;
        }
        
        core = (Core) corePlugin;
        
        // Use Core APIs
        CoreColorAPI colorAPI = core.getColorAPI();
        CoreMessageAPI messageAPI = core.getMessageAPI();
        
        // Example: Send a colored message
        Player player = getServer().getPlayer("PlayerName");
        if (player != null) {
            messageAPI.sendMessage(player, "&aHello from Core API!");
        }
    }
}
```

## Requirements

- **Minecraft Versions**: 1.16, 1.17, 1.18, 1.19, 1.20, 1.21+
- **Java Version**: 21
- **Server Types**: Bukkit, Spigot, Paper

## Documentation

For detailed API documentation and examples, please refer to the main project documentation (if available) or check the source code.

## Support

- **Website**: https://rhavenside.de
- **Author**: Rhaven
- **Version**: Check the latest release tag

## License

This project is provided as-is. Please refer to the license file for details.

---

**Note**: This repository only contains releases. For issues, feature requests, or contributions, please contact the maintainer through the appropriate channels.

