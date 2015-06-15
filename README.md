ACS Embedded Twitter4J API
==========================

This projects makes the [Twitter4J](http://twitter4j.org/) API available as an OSGi bundle inside a content package suitable for deployment on CQ/AEM.

## Installation

### Snapshot releases

To compile and install a snapshot release use the autoInstallPackage Maven profile:

`mvn clean install -PautoInstallPackage`

### Stable releases

Stable releases are available [from the GitHub releases page](https://github.com/Adobe-Consulting-Services/com.adobe.acs.bundles.twitter4j/releases) and can be installed manually using CRX Package Manager like any other package. However, most likely you'll be using Twitter4J as part of a larger project in which case you many want to include it as part of your Maven build cycle.

To add the ACS Embedded Twitter4J API to your Maven build first add the dependency to the `<dependencies>` section of your content project's pom.xml file:

```
<dependency>
    <groupId>com.adobe.acs.bundles</groupId>
    <artifactId>com.adobe.acs.bundles.twitter4j-content</artifactId>
    <version>1.0.0</version>
    <type>zip</type>
</dependency>
```

Then, (while still in the content project’s pom.xml) within the configuration of the content-package-maven-plugin, add an `embedded`:

```
<plugin>
    <groupId>com.day.jcr.vault</groupId>
    <artifactId>content-package-maven-plugin</artifactId>
    <extensions>true</extensions>
    <configuration>
        ...
        <embeddeds>
            <embedded>
                <groupId>com.adobe.acs.bundles</groupId>
                <artifactId>com.adobe.acs.bundles.twitter4j-content</artifactId>
                <target>/apps/system/install</target>
            </embedded>
        </embeddeds>
        ...
    </configuration>
</plugin>
```

Finally, in the `<dependencies>` section of the pom.xml for any Maven modules that will use Twitter APIs add the dependency for the Twitter4J bundle:

```
<dependency>
    <groupId>com.adobe.acs.bundles</groupId>
    <artifactId>com.adobe.acs.bundles.twitter4j-content</artifactId>
    <version>1.0.0</version>
    <scope>provided</scope>
</dependency>
```