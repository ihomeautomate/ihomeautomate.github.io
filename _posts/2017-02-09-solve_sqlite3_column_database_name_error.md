---
title: Solving sqlite3 column database name error(s)
author: iHomeAutomate
excerpt: 'sqlite3 on mac with mono, solved!'
layout: article
permalink: /2017/02/09/solve_sqlite3_column_database_name_error/
categories:
  - homeseer
tags:
  - homeseer3
  - hs3
  - dotnet
  - csharp
  - mono
  - sqlite3
  - sqlite
comments: true
ads: true
image:
  teaser: 2017/02/sqlite3.png
---
Running HS3 on osx has issues showing its logs. The console displays following error: 
{% highlight bash %}
[Error]->GetLog Error: sqlite3_column_database_name16
{% endhighlight %}

It looked like a typical mono on mac issue, and easily resolved by recompiling the sqlite binary with the `SQLITE_ENABLE_COLUMN_METADATA` directive.
It's not a specific homeseer problem, it's applicable to all mono on mac users using `System.Data.SQLite.dll`

* Be sure to have all developer tools installed
* Download source code from [sqlite.org](http://sqlite.org/download.html) (should be sqlite-autoconf-*.tar.gz)
* Unzip

Compile with correct options, i386 arch was needed because mono was still compiled with x86 architecture.
{% highlight bash %}
./configure CFLAGS='-arch x86_64 -arch i386 -DSQLITE_ENABLE_COLUMN_METADATA=1' && make
{% endhighlight %}


The resulted `.libs/libsqlite3.0.dylib` is identified as :
{% highlight bash %}
libsqlite3.0.dylib: Mach-O universal binary with 2 architectures: [x86_64: Mach-O 64-bit dynamically linked shared library x86_64] [i386]
{% endhighlight %}

... and can then be copied in the same folder as the mono application, in our case the homeseer folder.
 
Restart the application, problem should be solved :-).
