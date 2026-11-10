# Fabric 26.2 port — work in progress

Target: Fabric 26.2, followed by a separate NeoForge 26.2 + Sinytra Connector compatibility test.
Based on upstream 26.3 commit `977cfb4674ce1e91553375ea0c211d6247bb63ce`.

## Completed

- Pin Minecraft and optional integration dependencies to 26.2 releases.
- Use a distinct experimental artifact version and exclude Minecraft 26.3 in mod metadata.
- Restore the 26.2 Gui mixin target and hotbar injection, screen navigation, raid HUD ticks, and music toast access.
- Trigger CI on build configuration, resources, and workflow changes; use Temurin Java 25.

## Validation status

No working JAR has been produced or tested. Local Gradle 9.6.0 runs under Temurin 25.0.1 and resolves build plugins, but Loom initialization fails before compilation:

```
net.fabricmc.loom.util.CurrentPlatform.isUnixDomainSocketsSupported
java.net.SocketException: Operation not permitted
```

This is an execution-environment restriction, not a compiler diagnostic. Run `./gradlew build` with Java 25 in GitHub Actions or an unrestricted development environment to obtain actionable compiler errors.

## Remaining work

- Adapt rendering pipelines, entity rendering, particles, advancements, block codecs, recipes, and world generation APIs/resources changed by upstream's 26.3 migration.
- Review upstream migration commits `4930c491`, `d159f528`, `20845145`, `3cbc357a`, `2f4c2880`, `f37193d6`, `23c65515`, `ca2f2fca`, `da6798e3`, `7f442a26`, and `d3dab4ad`. Preserve later gameplay additions; do not blindly revert entire commits.
- Compile both main and client sources and verify mixin targets.
- Launch Fabric 26.2: menu, new world, plants, projectiles, raids, dimensions, save/reload.
- Test Connector separately in a disposable world, then check the existing modpack and Solas Shader.

Dependency versions were checked against Modrinth's Fabric / Minecraft 26.2 version listings: Fabric API `0.161.0+26.2`, TerraBlender `26.2.0.0.2`, Iris `1.11.4+26.2-fabric`, Mod Menu `20.0.3`.
