# Farmer's Delight 1.12.2 Port Setup Instructions

This branch has been configured for Minecraft 1.12.2 with Forge. Below are the instructions to set up and develop the mod.

## Configuration Changes

The following changes have been made to port the project to Minecraft 1.12.2:

1. **Gradle Configuration**
   - Updated to Gradle 4.10.3 (compatible with ForgeGradle 2.3)
   - Configured ForgeGradle 2.3-SNAPSHOT for Minecraft 1.12.2
   - Set Java 8 compatibility (sourceCompatibility and targetCompatibility)

2. **Minecraft & Forge Versions**
   - Minecraft: 1.12.2
   - Forge: 14.23.5.2859 (recommended stable version)
   - JEI: 4.16.1.301 (for 1.12.2)

3. **Project Structure**
   - Converted `mods.toml` to `mcmod.info` (1.12.2 format)
   - Added `pack.mcmeta` with pack_format 3
   - Removed Mixins configuration (not standard for 1.12.2)
   - Removed Access Transformers references

## Setting Up the Development Environment

### Prerequisites
- Java 8 JDK (OpenJDK or Oracle JDK)
- IntelliJ IDEA (Community or Ultimate Edition)

### Step 1: Setup Forge Workspace

Run the following command in the project root directory:

```bash
./gradlew setupDecompWorkspace
```

This will:
- Download Minecraft and Forge
- Decompile Minecraft source code
- Apply Forge patches
- Setup the development workspace

**Note:** This process can take 10-30 minutes depending on your internet speed and computer.

### Step 2: Generate IDE Configuration

For IntelliJ IDEA, run:

```bash
./gradlew genIntellijRuns
```

Or if that doesn't work with ForgeGradle 2.3, use:

```bash
./gradlew idea
```

### Step 3: Import into IntelliJ IDEA

1. Open IntelliJ IDEA
2. Select "Open" or "Import Project"
3. Navigate to the project directory and select it
4. IntelliJ will detect the Gradle project and import it
5. Wait for IntelliJ to finish indexing

### Step 4: Configure Run Configurations

In IntelliJ IDEA:

1. Go to **Run > Edit Configurations**
2. Click the **+** button and select **Application**
3. For the **Client**:
   - Name: `Minecraft Client`
   - Main class: `GradleStart`
   - Working directory: `%MODULE_WORKING_DIR%/run`
   - Use classpath of module: `FarmersDelight_main`

4. For the **Server**:
   - Name: `Minecraft Server`
   - Main class: `GradleStartServer`
   - Working directory: `%MODULE_WORKING_DIR%/run`
   - Use classpath of module: `FarmersDelight_main`

## Building the Mod

To build the mod JAR file:

```bash
./gradlew build
```

The compiled mod will be located in `build/libs/FarmersDelight-1.12.2-1.0.0.jar`

## Important Notes

### Code Compatibility

The Java source code in this project is currently written for Minecraft 1.20.1. You will need to update it for 1.12.2 compatibility:

1. **Package Changes:**
   - Minecraft 1.20.1 uses newer package structures
   - 1.12.2 uses older package names (e.g., `net.minecraft.item` instead of `net.minecraft.world.item`)

2. **API Changes:**
   - Many Minecraft APIs have changed between 1.12.2 and 1.20.1
   - Registry system is different
   - Event handling has changed
   - Block/Item registration is different

3. **Removed Features:**
   - Mixins are not standard in 1.12.2 (removed from this configuration)
   - Many modern Forge features don't exist in 1.12.2

### Recommended Approach

For a full 1.12.2 port, you may want to:

1. Start with a fresh 1.12.2 Forge MDK
2. Manually port features from the 1.20.1 version
3. Reference 1.12.2 mod examples for API usage

### Troubleshooting

**Issue: `maven.minecraftforge.net: No address associated with hostname`**
- This is a network issue. Ensure you have internet access and can reach Forge's Maven repository.
- Try using a VPN if the repository is blocked in your region.

**Issue: Java version mismatch**
- Ensure you're using Java 8 for Minecraft 1.12.2
- Set `JAVA_HOME` environment variable to Java 8 installation

**Issue: Gradle daemon issues**
- Run `./gradlew --stop` to stop all Gradle daemons
- Delete `.gradle` directory and try again

## Next Steps

1. Review the Java source code in `src/main/java/`
2. Update package imports for 1.12.2
3. Update registry code to use 1.12.2 APIs
4. Test the mod in-game
5. Fix any compilation or runtime errors

## Resources

- [Forge 1.12.2 Documentation](https://mcforge.readthedocs.io/en/1.12.x/)
- [Minecraft Forge Forums](https://forums.minecraftforge.net/)
- [1.12.2 Example Mods](https://github.com/TheGreyGhost/MinecraftByExample/tree/1-12-2)

## License

This mod is licensed under the MIT License. See LICENSE file for details.
