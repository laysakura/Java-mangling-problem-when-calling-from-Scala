# Java mangling problem when calling from Scala

I found that when a Java class is deeply nested, the class cannot be used from Scala due to a "mangling" problem.
(Although I'm not sure it is called "mangling" in Java world)

`JavaMain` in the source tree works good but `ScalaMain` fails with the following runtime error.

```java
Exception in thread "main" java.lang.NoClassDefFoundError: com/laysakura/toooooo/looooong/pkg/Klass1$Klass2$K$$$$bfa12ff97d5826532af518f480616ad2$$$$Klass15$Klass16
	at ScalaMain$.main(ScalaMain.scala:5)
	at ScalaMain.main(ScalaMain.scala)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at com.intellij.rt.execution.application.AppMain.main(AppMain.java:147)
Caused by: java.lang.ClassNotFoundException: com.laysakura.toooooo.looooong.pkg.Klass1$Klass2$K$$$$bfa12ff97d5826532af518f480616ad2$$$$Klass15$Klass16
	at java.net.URLClassLoader.findClass(URLClassLoader.java:381)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:424)
	at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:331)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:357)
	... 7 more

Process finished with exit code 1
```

You can see `Klass1$Klass2$K$$$$bfa12ff97d5826532af518f480616ad2$$$$Klass15$Klass16` .
It seems to be mangled.
