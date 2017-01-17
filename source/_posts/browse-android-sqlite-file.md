---
title: Browsing your Android app's SQLite file
date: 2017-01-04 21:01:38
tags:
- android
- database
- tips
---

There is no easy way to see the contents of your Android app’s database unless your device is rooted. If it is not rooted, you can first copy your database file to a sdcard (whether real or simulated) and then copy it back to your computer. You can then use any SQLite browser app such as [Firefox’s SQLite Manager](https://addons.mozilla.org/en-us/firefox/addon/sqlite-manager/) to browse the contents. These are the steps you need: ...

<!--more-->

1) Add the following helper function somewhere in your code (doesn’t matter where you put it; it’s a static function):

```java
public static void copyDatabase(String packageName, String dbName) {
    try {
        File dbFile = new File(String.format("/data/data/%s/databases/%s", packageName, dbName));
        if (dbFile.exists()) {
            File dbDestFile = new File(String.format("%s/%s", Environment.getExternalStorageDirectory().getAbsoluteFile(), dbName));
            dbDestFile.createNewFile();
            InputStream in = new FileInputStream(dbFile);
            OutputStream out = new FileOutputStream(dbDestFile);
            byte[] buf = new byte[1024];
            int len;
            while ((len = in.read(buf)) > 0) {
                out.write(buf, 0, len);
            }
            in.close();
            out.close();
        }
    } catch (Exception e) {
        Log.e("database_copy", e.getLocalizedMessage());
    }
}
```

2) Call the above function somewhere from your main activity:

```java
...
copyDatabase(getPackageName(), "databasename.db");
...
```

3) The above 2 steps just copies your database file to your device’s sdcard. You need to copy this file now back to your computer. We’ll use `adb pull` to do it. From your terminal:


```shell
adb pull /sdcard/databasename.db ~/Desktop
```

The database file should now be copied to your desktop.