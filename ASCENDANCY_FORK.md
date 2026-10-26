# Ascendancy Expansion fork

MIT-licensed fork of DonovanDMC/ProjectExpansion, initially pinned to Minecraft
Java 1.21.1 / NeoForge. The original copyright and LICENSE stay intact. This
work is unofficial and not endorsed by ProjectE or the original developer.

## Compatibility
Keep mod ID projectexpansion and existing block/item registry identifiers.
This fork is a REPLACEMENT for the original JAR, not a new addon to install
alongside it. Never install both; safeguard the world before a version switch.
Do not change item IDs without a migration. GitHub work has NO effect on the
running Minecraft instance.

## Two release channels
1. Pushes and pull requests to 1.21.1 trigger GitHub-hosted builds using
   Java 21, Node asset generation, and NeoForge Gradle. Successful runs upload
   a testable JAR and its SHA256SUMS as temporary workflow artifacts.
2. To issue a test prerelease, change mod_version to a unique Ascendancy version,
   merge the source into 1.21.1 after CI passes, then tag the exact commit with
   asc-v followed by that mod_version (e.g., asc-v1.0.6-asc.1).
   GitHub rebuilds that pinned commit and publishes a GitHub prerelease with a
   SHA256 checksum. A prerelease is NOT automatically declared stable.
3. Test the prerelease in a disposable test world or safeguarded copy. Validate
   existing power flowers, storage, EMC, recipes, inventory and new mechanics.
   Once tested, edit the SAME GitHub Release and uncheck "Set as a pre-release".
   That promotes the EXACT tested JAR, with no fresh build or changed checksum.

No local compiling required: the OptiPlex stores canonical source/documents;
the Dell is the Minecraft runtime test machine. The first feature under
consideration is restoration of classic Final Star duplication. It is not
implemented or enabled by this infrastructure change. The much larger idea of
combining dozens of mods is explicitly out of scope.

## Build note: upstream signing task
The upstream Gradle build finalizes JAR creation with its private `signJar` task.
Our Actions build explicitly excludes `signJar` because we do not possess or use
the upstream author's private signing credentials. This produces an unsigned,
reproducibly identified, SHA256-checksummed JAR without trying to sign it.
