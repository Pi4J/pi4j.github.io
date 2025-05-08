---
title: "Starting with a Desktop Icon"
date: 2025-05-07
tags: ["UI"]
---

2025-05-07 by Frank Delporte

**Richard Norrie** created an oscilloscope with Pi4J and was looking for a way to start his application with a desktop icon. Unfortunately, he ran into a few issues as the icon led to "Java not found" error. This was likely due to environment variables not being properly set in the desktop launcher context. 

Here are the steps how this got fixed as you can see in this screenshot:

![](/assets/blogs/desktop-icon/oscilloscope-v2.png)

1. Ensure Java is properly installed and the PATH is set system-wide:

```bash
echo 'export JAVA_HOME=/path/to/your/java' >> ~/.bashrc
echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

2. Create a desktop entry file (with `.desktop extension`) in `~/.local/share/applications/` or `/usr/share/applications/`:

```text
[Desktop Entry]
Name=Oscilloscope
Type=Application
Exec=bash -ic '/path/to/your/script.sh'
Icon=/path/to/an/icon.png
Terminal=false
Categories=Application
```

The key parts here are:

* Using `bash -ic` which ensures the bash environment (including PATH) is properly loaded.
* Using absolute paths for both the `Exec` and `Icon` entries.
* The `script.sh` should also use absolute paths to the Java jar file.

3. Make both your shell script and the `.desktop` file executable:

```bash
chmod +x /path/to/your/script.sh
chmod +x /path/to/your/oscilloscope.desktop
```

4. Your shell script should point to the full path of your `.jar` file:

```text
#!/bin/bash
java -jar /full/path/to/oscilloscope.jar
```

This approach ensures all necessary environment variables are properly set regardless of how the application is launched.
