# JDK Bin Tools Reference

> A quick reference for every tool in `$JAVA_HOME/bin` — what it does and a simple example.

---

## All Available Commands

| Tool | Category | What it does |
|---|---|---|
| `jar` | Package | Create / manage JAR archives |
| `jarsigner` | Security | Sign or verify JARs |
| `java` | Run | Run a class, JAR, or source file |
| `javac` | Compile | Compile `.java` → `.class` |
| `javadoc` | Compile | Generate HTML docs from comments |
| `javap` | Compile / Debug | Disassemble `.class` files |
| `jcmd` | Monitor | All-in-one live JVM diagnostics |
| `jconsole` | Monitor | GUI JMX monitor |
| `jdb` | Debug | Command-line debugger |
| `jdeprscan` | Compile | Find deprecated API usage in a JAR |
| `jdeps` | Compile | Show module/package dependencies |
| `jfr` | Monitor | Production profiler (Flight Recorder) |
| `jhsdb` | Debug | Post-mortem crash analysis |
| `jimage` | Package | Inspect JDK module images |
| `jinfo` | Debug | Show JVM flags of a running process |
| `jlink` | Package | Build a custom minimal JRE |
| `jmap` | Debug | Heap dump — diagnose memory leaks |
| `jmod` | Package | Create JMOD module packages |
| `jnativescan` | Native | Scan for restricted native method usage |
| `jpackage` | Package | Build native OS installers |
| `jps` | Monitor | List running Java processes |
| `jrunscript` | Run | Run scripts from CLI |
| `jshell` | Run | Interactive Java REPL |
| `jstack` | Debug | Thread dump — diagnose hangs/deadlocks |
| `jstat` | Monitor | Stream GC / class loading stats |
| `jstatd` | Monitor | Daemon for remote monitoring |
| `jwebserver` | Run | One-command static file server |
| `keytool` | Security | Manage keystores and certificates |
| `native-image` | Native (GraalVM) | Compile Java to native binary |
| `native-image-configure` | Native (GraalVM) | Generate reflection config for native-image |
| `native-image-inspect` | Native (GraalVM) | Inspect native binary contents |
| `rmiregistry` | Legacy | RMI naming registry |
| `serialver` | Legacy | Get `serialVersionUID` for a class |

---

## Examples

### `jar` — Create and manage JARs

```bash
jar --create --file app.jar --main-class Hello Hello.class   # create a JAR
java -jar app.jar                                             # run it
jar --list --file app.jar                                     # list contents
jar --extract --file app.jar                                  # unzip
jar --update --file app.jar Hello.class                       # update a file inside
```

---

### `jarsigner` — Sign or verify a JAR

```bash
# sign
jarsigner -keystore keystore.jks app.jar mykey

# verify
jarsigner -verify -verbose app.jar
```

---

### `java` — Run your application

```bash
java Hello                    # run a compiled class
java -jar myapp.jar           # run a JAR
java Hello.java               # run a single file directly (Java 11+)
java -Xmx512m -jar myapp.jar  # run with 512 MB heap limit
```

---

### `javac` — Compile source files

```java
// Hello.java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

```bash
javac Hello.java              # produces Hello.class
javac -d out/ src/**/*.java   # compile whole folder into out/
```

---

### `javadoc` — Generate HTML API docs

```java
/**
 * Simple calculator utility.
 * @author Dev
 */
public class Calculator {
    /** Adds two numbers. @param a first @param b second @return sum */
    public int add(int a, int b) { return a + b; }
}
```

```bash
javadoc -d docs/ Calculator.java
# open docs/index.html in a browser
```

---

### `javap` — Disassemble `.class` files

```bash
javap Hello              # show public method signatures
javap -c Hello           # show bytecode instructions
javap -p -verbose Hello  # show everything including private members
```

---

### `jcmd` — Live JVM diagnostics

```bash
jcmd                          # list all running JVM processes
jcmd 12345 help               # list available commands for that process
jcmd 12345 Thread.print       # thread dump
jcmd 12345 GC.run             # force garbage collection
jcmd 12345 VM.flags           # print all JVM flags
jcmd 12345 GC.heap_info       # heap summary
```

> Prefer `jcmd` over the older `jmap`/`jstack` on modern JDKs.

---

### `jconsole` — GUI JMX monitor

```bash
jconsole                      # open GUI, pick a local process
jconsole hostname:9999        # connect to a remote JVM
```

```bash
# Enable JMX on app startup for remote access
java -Dcom.sun.management.jmxremote \
     -Dcom.sun.management.jmxremote.port=9999 \
     -Dcom.sun.management.jmxremote.authenticate=false \
     -jar myapp.jar
```

---

### `jdb` — Command-line debugger

```bash
javac -g Hello.java    # compile with debug info first
jdb Hello
```

```
> stop in Hello.main   # set a breakpoint
> run                  # start execution
> next                 # step to next line
> print x              # inspect a variable
> cont                 # continue execution
> quit
```

---

### `jdeprscan` — Find deprecated API usage

```bash
jdeprscan --release 21 myapp.jar   # scan against Java 21 deprecations
jdeprscan --release 21 --list      # list all deprecated APIs in Java 21
```

---

### `jdeps` — Analyze dependencies

```bash
jdeps myapp.jar                      # show all dependencies
jdeps --jdk-internals myapp.jar      # find internal JDK API usage
jdeps --print-module-deps myapp.jar  # summarize by module
```

---

### `jfr` — Java Flight Recorder

```bash
# start recording on a running JVM
jfr start name=myrec filename=out.jfr jvm=12345

# stop and save
jfr stop name=myrec jvm=12345

# print summary from CLI
jfr print out.jfr

# or enable at JVM startup
java -XX:StartFlightRecording=filename=out.jfr,duration=60s -jar myapp.jar
```

> Open `out.jfr` in JDK Mission Control for flame graphs and GC analysis.

---

### `jhsdb` — Post-mortem / crash debugger

```bash
jhsdb hsdb --pid 12345                                         # GUI — attach to live process
jhsdb jstack --pid 12345                                       # thread dump via jhsdb
jhsdb jstack --core core.1234 --exe $JAVA_HOME/bin/java        # analyze a core dump
```

---

### `jimage` — Inspect JDK module images

```bash
jimage list $JAVA_HOME/lib/modules                    # list all modules
jimage extract --dir ./out $JAVA_HOME/lib/modules     # extract to a folder
jimage info $JAVA_HOME/lib/modules                    # show image metadata
```

---

### `jinfo` — JVM flags and system properties

```bash
jinfo 12345                        # print all JVM info
jinfo -flag MaxHeapSize 12345      # check a specific flag
jinfo -sysprops 12345              # list all system properties
```

---

### `jlink` — Build a custom minimal JRE

```bash
jlink \
  --module-path $JAVA_HOME/jmods \
  --add-modules java.base,java.logging,java.sql \
  --compress 2 \
  --output my-runtime

my-runtime/bin/java -jar myapp.jar   # run with the custom JRE
```

---

### `jmap` — Heap dumps and memory maps

```bash
jmap -heap 12345                               # heap summary
jmap -dump:format=b,file=heap.hprof 12345      # full heap dump
jmap -histo 12345 | head -20                   # top memory consumers
```

> Open `heap.hprof` in VisualVM or Eclipse MAT to find memory leaks.

---

### `jmod` — Create JMOD module packages

```bash
jmod create \
  --class-path mods/com.example \
  --main-class com.example.Main \
  com.example.jmod

jmod list com.example.jmod       # list contents
jmod describe com.example.jmod   # describe the module
```

---

### `jnativescan` — Scan for restricted native calls *(Java 22+)*

```bash
jnativescan --class-path myapp.jar

jnativescan --module-path mods/ --add-modules com.example
```

---

### `jpackage` — Build native installers

```bash
# macOS .dmg
jpackage --input lib/ --main-jar myapp.jar \
  --main-class com.example.Main --name MyApp --type dmg

# Windows .msi
jpackage --input lib/ --main-jar myapp.jar --name MyApp --type msi

# Linux .deb
jpackage --input lib/ --main-jar myapp.jar --name myapp --type deb
```

---

### `jps` — List running Java processes

```bash
jps          # pid + main class name
jps -v       # include JVM arguments
jps -l       # full main class name
```

> Always run this first to get the PID before using `jcmd`, `jstack`, `jmap`, etc.

---

### `jrunscript` — Run scripts from CLI

```bash
jrunscript -e "print('hello')"   # one-liner
jrunscript myscript.js           # run a script file
```

---

### `jshell` — Interactive Java REPL

```bash
$ jshell
jshell> int x = 10;
jshell> System.out.println(x * x);    // 100
jshell> var list = List.of(1, 2, 3);
jshell> list.stream().map(n -> n * 2).toList()
jshell> /open utils.java              // load a file into the session
jshell> /exit
```

---

### `jstack` — Thread dump

```bash
jps                              # find the PID first
jstack 12345                     # print all thread traces
jstack 12345 > threads.txt       # save to file for analysis
jstack -l 12345                  # include lock info for deadlock detection
```

---

### `jstat` — Real-time JVM statistics

```bash
jstat -gc 12345 1000        # GC stats every 1 second
jstat -gcutil 12345 1000    # GC utilisation as percentages
jstat -class 12345          # class loading stats
jstat -compiler 12345       # JIT compiler activity
```

---

### `jstatd` — Remote monitoring daemon

```
# jstatd.policy
grant codebase "file:${java.home}/../lib/tools.jar" {
    permission java.security.AllPermission;
};
```

```bash
jstatd -J-Djava.security.policy=jstatd.policy   # start the daemon
jstat -gc //remotehost/12345 1000               # connect remotely
```

---

### `jwebserver` — Static HTTP file server *(Java 18+)*

```bash
jwebserver                          # serve current dir on port 8000
jwebserver -p 9090 -d ./public      # custom port and directory
jwebserver -b 0.0.0.0 -p 8080      # bind to all network interfaces
```

---

### `keytool` — Manage keystores and certificates

```bash
# generate a key pair (self-signed certificate)
keytool -genkeypair -alias mykey -keyalg RSA -keysize 2048 \
  -validity 365 -keystore keystore.jks

# list all entries in a keystore
keytool -list -keystore keystore.jks

# import a CA certificate
keytool -importcert -alias myca -file ca.crt -keystore truststore.jks

# export a certificate to a file
keytool -exportcert -alias mykey -file mycert.crt -keystore keystore.jks
```

---

### `native-image` — Compile Java to a native binary *(GraalVM)*

```bash
native-image -jar myapp.jar        # compile a JAR

./myapp                            # run — no JVM needed!

# with reflection configuration
native-image -H:ReflectionConfigurationFiles=reflect.json -jar myapp.jar
```

---

### `native-image-configure` — Generate reflection/JNI config *(GraalVM)*

```bash
# step 1: run your app with the tracing agent
java -agentlib:native-image-agent=config-output-dir=config/ -jar myapp.jar

# the agent creates these files in config/
#   reflect-config.json
#   jni-config.json
#   resource-config.json

# step 2: use the configs in the native-image build
native-image -H:ConfigurationFileDirectories=config/ -jar myapp.jar
```

---

### `native-image-inspect` — Inspect native binary contents *(GraalVM)*

```bash
native-image-inspect --list-classes ./myapp    # all included classes
native-image-inspect --list-methods ./myapp    # all included methods
```

---

### `rmiregistry` — RMI naming registry *(legacy)*

```bash
rmiregistry          # start on default port 1099
rmiregistry 2000     # start on a custom port
```

```java
// register a remote object in code
Registry reg = LocateRegistry.getRegistry(1099);
reg.bind("MyService", myRemoteObject);
```

---

### `serialver` — Get serialVersionUID *(legacy)*

```bash
serialver com.example.MyModel
# output:
# com.example.MyModel: static final long serialVersionUID = -1234567890123456789L;
```

```java
// paste the result into your class
public class MyModel implements Serializable {
    static final long serialVersionUID = -1234567890123456789L;
    // ...
}
```

---

*Prepared for the Java Community of Practice.*
