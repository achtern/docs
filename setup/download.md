# Download the binaries

Downloading the binaries directly without maven is not supported yet. Stay tuned!

This will have to wait for a proper build server, which will generate nightly builds as well!

For now you can download the binaries this way:

```shell
# download the AchternEngine class and resource files only.
curl -L -O https://search.maven.org/remotecontent?filepath=org/achtern/AchternEngine/0.4/AchternEngine-0.4.jar
```

[Direct Link](https://search.maven.org/remotecontent?filepath=org/achtern/AchternEngine/0.4/AchternEngine-0.4.jar)

But if you need the dependencies as well you can use ivy to get the job done.

```shell
# download the AchternEngine class and resource files only.
curl -L -O https://search.maven.org/remotecontent?filepath=org/achtern/AchternEngine/0.4/AchternEngine-0.4.jar
# download iyy
curl -L -O https://search.maven.org/remotecontent?filepath=org/apache/ivy/ivy/2.4.0/ivy-2.4.0.jar
# run ivy
java -jar ivy-2.4.0.jar -dependency com.sparkjava spark-core 2.1 -retrieve "AchternEngine-0.4.jar"
```

However it is strongly recommended to go for a proper maven project for now!
