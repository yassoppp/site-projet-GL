---
title: Questions fréquentes avec Maven pour le projet GL
---

{{< toc >}}

## `mvn compile` donne une erreur `Could not find artifact com.sun:tools:jar:0`

Sous Mac OS X, il peut arriver qu'on obtienne l'erreur suivante :

```
[ERROR] Failed to execute goal on project Deca: Could not resolve dependencies for project fr.ensimag:Deca:jar:0.0.1-SNAPSHOT: Could not find artifact com.sun:tools:jar:0 at specified path /System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home/../lib/tools.jar -> [Help 1]
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/DependencyResolutionException
```

En effet, le plugin `Cobertura` nécessite le fichier `tools.jar` qui devrait être fourni avec le
**JDK**, mais ne l'est pas toujours.

Vérifiez que vous avez bien installé un **JDK** et non un **JRE**, et faites pointer la variable
`$JAVA_HOME` sur le répertoire d'installation du **JDK**.

Une solution est d'ajouter explicitement `tools.jar` à votre `pom.xml` (en faisant un cas
particulier pour Mac OS, pour ne pas perturber la compilation sur les autres plateformes) :

```Diff
--- a/pom.xml
+++ b/pom.xml
@@ -12,6 +12,25 @@
     <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
     <compileSource>1.6</compileSource>
   </properties>
+  <profiles>
+    <profile>
+      <id>osx_profile</id>
+      <activation>
+       <os>
+         <family>mac</family>
+       </os>
+      </activation>
+      <dependencies>
+       <dependency>
+         <groupId>com.sun</groupId>
+         <artifactId>tools</artifactId>
+         <version>1.6</version>
+         <scope>system</scope>
+         <systemPath>${java.home}/../Classes/classes.jar</systemPath>
+       </dependency>
+      </dependencies>
+    </profile>
+  </profiles>
   <dependencies>

     <dependency>
```

Si cela ne marche pas, une autre solution est d'utiliser un plugin `Cobertura` plus ancien, qui n'a
pas ce problème.
C'est possible en appliquant ce patch à votre projet :

```Diff
--- a/pom.xml
+++ b/pom.xml
@@ -50,7 +50,7 @@
           runtime -->
       <groupId>net.sourceforge.cobertura</groupId>
       <artifactId>cobertura</artifactId>
-      <version>2.0.3</version>
+      <version>1.9.4.1</version>
       <!-- we do not want to include Cobertura in generated packages
            (e.g. jar-with-dependencies) -->
       <scope>test</scope>
@@ -93,7 +93,7 @@
        <!-- mvn cobertura:cobertura to generate coverage report (instrument, test and report)
             mvn cobertura:instrument to instrument classes.
        -->
-       <version>2.6</version>
+       <version>2.5.2</version>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>cobertura-maven-plugin</artifactId>
        <configuration>
```

Si vous possédez plusieurs versions de **JDK** et **JRE** sur votre Mac, notamment la 1.6 et 1.7, il
peut arriver que **NetBeans** (ou **Eclipse**) utilise une version différente de Java que maven en
ligne de commande.
Pour utiliser uniquement la version 1.7 et corriger le problème de Cobertura il faut modifier le
`pom.xml` de cette façon :
```Diff
--- a/pom.xml
+++ b/pom.xml
@@ -12,6 +12,25 @@
     <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
     <compileSource>1.6</compileSource>
   </properties>
+  <profiles>
+    <profile>
+      <id>osx_profile</id>
+      <activation>
+       <os>
+         <family>mac</family>
+       </os>
+      </activation>
+      <dependencies>
+       <dependency>
+         <groupId>com.sun</groupId>
+         <artifactId>tools</artifactId>
+         <version>${java.version}</version>
+         <scope>system</scope>
+         <systemPath>${java.home}/../lib/tools.jar</systemPath>
+       </dependency>
+      </dependencies>
+    </profile>
+  </profiles>
   <dependencies>

     <dependency>
```

Cette modification permet de faire pointer votre IDE vers le bon fichier `tools.jar` que demande
`maven` en précisant la bonne version à utiliser.

Il faut ensuite modifier votre variable d'environnement `JAVA_HOME` dans votre `.bash_profile` afin
que maven puisse savoir quelle version de Java il doit utiliser.
Éditer le fichier `.bash_profile` dans votre `home` et ajoutez :

```Shell
export JAVA_HOME=`/usr/libexec/java_home -v 1.7`
```

Pensez à relancer votre `Terminale` pour prendre en compte la modification du `.bash_profile`,
normalement **Maven** devrait compiler avec la version 1.7 de Java en ligne de commande et sous
**NetBeans** (et même **Eclipse**).

## Comment accélérer Maven et économiser de l'espace disque

Par défaut, Maven télécharge et conserve les dépendances et plugins dans le répertoire
`~/.m2/repository/`.
Sur les machines de l'école, cela a plusieurs conséquences :
* Le répertoire est partagé via NFS, donc un peu plus lent qu'un disque local
* Ce répertoire utilise de l'espace disque dans votre répertoire personnel (et donc compte dans
votre quota, ce qui peut être problématique si on a beaucoup de dépendances)

Une solution est de stocker ce cache sur le disque local de la machine, dans un répertoire
temporaire.
Pour cela, créer un fichier `~/.m2/settings.xml` avec le contenu suivant :

```XML
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                      http://maven.apache.org/xsd/settings-1.0.0.xsd">
  <localRepository>/var/tmp/${user.name}/m2/repository</localRepository>
```

Une fois ce fichier créé, vous pouvez supprimer le répertoire `~/.m2/repository` sans risque.

Cette solution résous les deux problèmes ci-dessus.
En contrepartie, il faudra re-télécharger le cache pour chaque machine que vous utiliserez.
Cette manipulation n'a aucun intérêt sur une machine personnelle où `$HOME` est stocké sur le même
disque que `/var/tmp/`.

(Pour les curieux, la discussion qui a abouti à ce conseil se trouve
[ici](http://thread.gmane.org/gmane.comp.jakarta.turbine.maven.user/131606).)
