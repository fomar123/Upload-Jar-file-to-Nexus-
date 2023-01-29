# How to publish Using Gradle build tool: 
# You need to configure each build tool with Nexus credentials and address
# Add the following code snippet in the build.gradle file in your project.
# This file is also called the Gradle build script. The build configuration, tasks, and plugins are described in this file.
# Now we have to give user the Gradle or Maven credential to connnect with Nexus
# Add a plugin in the build.gradle and it will allow gradle to connect with nexus and push in repository

  apply plugin : 'maven-publish'

##### Now , add a publishing block
publishing {
publication { 

    }
repositories {

    }
}

# Publication block gives the info about jar file configuration
# Repositories block gives the info about the nexus repositories that we are going to upload our jar file

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

