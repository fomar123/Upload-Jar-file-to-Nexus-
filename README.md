# How to publish Using Gradle build tool: 

apply plugin : 'maven-publish'

##### Now , add a publishing block
publishing {
publication { 

    }
repositories {

    }
}

# Publication block gives the info about jar file configuration
##### Repositories block gives the info about the nexus repositories that we are going to upload our jar file

apply plugin: 'maven-publish'

publishing{
    publications{
        maven(MavenPublication){
            artifact("build/libs/my-app-$version"+".jar"){
                extension 'jar'
            }
        }
    }
    repositories {
        maven {
            name 'nexus'
            url "http://[your nexus ip]:[your nexus port]/repository/maven-snapshorts/"
            credentials {
                username xxx
                password xxx
            }
        }
    }
}

##### Add credentials in gradle.properties file
repoUser = "your username"
repoPassword = "your password"

##### Now, reference those credential in the build.gradle file

apply plugin: 'maven-publish'

publishing{
    publications{
        maven(MavenPublication){
            artifact("build/libs/my-app-$version"+".jar"){
                extension 'jar'
            }
        }
    }
    repositories {
        maven {
            name 'nexus'
            url "http://[your nexus ip]:[your nexus port]/repository/maven-snapshorts/"
            credentials {
                username project.repoUser
                password project.repoPasswd
            }
        }
    }
}

# Build the jar file
# Open your project folder in the terminal and build the jar file

   ./gradlew build
   
# Upload the Jar file to the repository

   ./gradlew publish

