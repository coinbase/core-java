# Coinbase Java Core — Deploy

Canonical repository: [coinbase/core-java](https://github.com/coinbase/core-java).

This project publishes through the [Sonatype Central Portal](https://central.sonatype.org/publish/publish-portal-maven/) (`central-publishing-maven-plugin` with server id `central`).

## Prerequisites

- JDK 11+
- Maven 3.8+
- GPG key configured (`gpg.keyname` in Maven settings or `pom.xml` properties)
- Sonatype Central user token ([generate in the portal](https://central.sonatype.com/account); use server id `central` in `~/.m2/settings.xml`)

## Publish with GitHub Actions

Creating a [GitHub Release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository#creating-a-release) runs [`.github/workflows/publish.yml`](.github/workflows/publish.yml). The workflow checks out the release tag, aligns `pom.xml` version with the tag (for example `v1.2.0` → `1.2.0`), runs Spotless and tests, then runs `mvn clean deploy`.

### Repository secrets

Configure these under **Settings → Secrets and variables → Actions**:

| Secret | Description |
|--------|-------------|
| `MAVEN_CENTRAL_USERNAME` | Sonatype Central token username |
| `MAVEN_CENTRAL_TOKEN` | Sonatype Central token password |
| `MAVEN_GPG_PRIVATE_KEY` | ASCII-armored GPG secret key (`gpg --armor --export-secret-keys KEY_ID`) |
| `MAVEN_GPG_PASSPHRASE` | Passphrase for that key |
| `MAVEN_GPG_KEY_ID` | GPG key id used by `maven-gpg-plugin` (`gpg.keyname`) |

### Release checklist

1. Bump `<version>` on `main` (or rely on the workflow to set it from the tag).
2. Create and push an annotated tag: `git tag v1.2.0 && git push origin v1.2.0`
3. Create a GitHub Release for that tag (event type **created** triggers publish).
4. Confirm the workflow succeeded and the artifact appears on [Maven Central](https://central.sonatype.com/artifact/com.coinbase.core/coinbase-core-java).

