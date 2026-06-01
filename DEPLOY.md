# Coinbase Java Core — Deploy

Canonical repository: [coinbase/core-java](https://github.com/coinbase/core-java).

Version **1.1.x** on [coinbase-samples/core-java](https://github.com/coinbase-samples/core-java) was the last samples-line release (git-only for 1.1.2). Publish **1.2.0+** from this repository.

## Prerequisites

- JDK 11+
- Maven 3.8+
- GPG key configured (`gpg.keyname` in Maven settings or `pom.xml` properties)
- Sonatype Central credentials (`central` server id in `~/.m2/settings.xml`)

## Publish to Maven Central

From a clean tree on the release tag:

```bash
git checkout v1.2.0
mvn clean deploy
```

Tag releases on `coinbase/core-java` after a successful publish:

```bash
git tag v1.2.0
git push pub v1.2.0
```
