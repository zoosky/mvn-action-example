# Maven Github Actions Example

Generated from [Maven in 5 Minutes](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html).

        mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false

Demos:

## Publish from local dev environment to Gitub repository


Setup your local .m2/settings.xml:

        <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
          https://maven.apache.org/xsd/settings-1.0.0.xsd">
          <!-- localRepository
           | The path to the local repository maven will use to store artifacts.
           |
           | Default: ${user.home}/.m2/repository
          <localRepository>/path/to/local/repo</localRepository>
          ${project.basedir} see https://cwiki.apache.org/confluence/display/MAVEN/Maven+Properties+Guide
          <localRepository>/Users/andreas/dev-local/maven/yves/.m2/repository</localRepository>
          -->
          <activeProfiles>
            <activeProfile>github</activeProfile>
          </activeProfiles>

          <profiles>
            <profile>
              <id>github</id>
              <repositories>
                <repository>
                  <id>central</id>
                  <url>https://repo1.maven.org/maven2</url>
                  <releases>
                    <enabled>true</enabled>
                  </releases>
                  <snapshots>
                    <enabled>true</enabled>
                  </snapshots>
                </repository>
                <repository>
                  <id>github</id>
                  <name>GitHub OWNER Apache Maven Packages</name>
                  <url>https://maven.pkg.github.com/zoosky/mvn-action-example</url>
                </repository>
              </repositories>
            </profile>
          </profiles>

          <servers>
            <server>
              <id>github</id>
              <username>zoosky</username>
              <password>bdcd5f60f4311a78663218e1b07359a188101256</password>
            </server>
          </servers>
        </settings>

Then, after configuring an appriate Github access token, you can publish to the repo. In this example to [https://github.com/zoosky?tab=packages](https://github.com/zoosky?tab=packages)

        mvn deploy -Dregistry=https://maven.pkg.github.com/zoosky -Dtoken=GH_TOKEN
        
## Create a release on Github and publish it direct to Github repository. 

See [.github/workflows/maven-publish.yml](.github/workflows/maven-publish.yml). Note that the Maven project is one level below the code repository's root dir.

      
