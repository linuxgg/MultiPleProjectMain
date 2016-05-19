# MultiPleProjectMain
Used for to show how use multiple project/modules in diff project. This is the Main project


#1.Used for what:
use multiple projects/modules, and easy to maintain.

#2.Environment:
##OS:
tom@tom-QTJ5:~$ sudo lsb_release -a
[sudo] password for tom: 
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 14.04.4 LTS
Release:	14.04
Codename:	trust

##IDE:
Android Studio 2.1
Build \#AI-143.2790544, built on April 22, 2016
JRE: 1.8.0_92-b14 amd64
JVM: Java HotSpot(TM) 64-Bit Server VM by Oracle Corporation

##Gradle:
tom@tom-QTJ5:/backup/lib/myExample/MultiPleProjectMain$ gradle -av 
------------------------------------------------------------
Gradle 2.10
------------------------------------------------------------

Build time:   2015-12-21 21:15:04 UTC
Build number: none
Revision:     276bdcded730f53aa8c11b479986aafa58e124a6

Groovy:       2.4.4
Ant:          Apache Ant(TM) version 1.9.3 compiled on December 23 2013
JVM:          1.8.0_92 (Oracle Corporation 25.92-b14)
OS:           Linux 4.2.0-36-generic amd64


#3.structure:
MultiPleProjectMain -- main project, use other project/modules
MultiPleProjectSub001 -- sub project, used in main project.

#4.what should pay attention to
>1.MultiPleProjectMain -> settings.gradle:
include(':MultipleProjectSub001')
project(':MultipleProjectSub001').projectDir = new File('/backup/lib/myExample/MultipleProjectSub001') //update the file path
include(':MultipleProjectSub001:java_lib')
include(':MultipleProjectSub001:androidlib')

>2.MultiPleProjectMain -> build.gradle(app):
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    testCompile 'junit:junit:4.12'
    compile 'com.android.support:appcompat-v7:23.4.0'
    compile 'com.android.support:design:23.4.0'
    compile  project(':MultipleProjectSub001:java_lib')
    compile  project(':MultipleProjectSub001:androidlib')
}

>3.If meet "Dexxxxxx" error when include Java_lib:
then: in build.gradle(java_lib)
""
apply plugin: 'java'

configurations{
    targetCompatibility='1.7'  //use jdk7, don't support jdk8
    sourceCompatibility='1.7'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
}
""
 
------------------------------------------------------------
====END & ENJOY
------------------------------------------------------------

