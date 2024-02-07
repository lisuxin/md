基本使用：

1. 切换到工程目录，即`build.gradle`所在的目录；
2. 运行`gradle --help`看看有哪些命令及选项；
3. 运行`gradle tasks`及`gradle tasks --all`看看有哪些任务可执行；
4. 运行`gradle run`执行程序；
5. 查看`build`目录有什么内容；
6. 运行`gradle clean`再看看`build`目录；
7. 运行`gradle jar`进行打包；
8. 切换到目录`build/libs`,看看有哪些jar包，试着运行一下看看；
9. 向`build.gradle`追加如下内容：

```gradle
jar {
    manifest {
        attributes(
                "Main-Class": "cn.edu.geely.dinosaur.main.Start",
                "Created-By": "Zhuo Nengwen"
        )
    }
}
```

1. 运行`gradle jar`；
2. 运行jar包看看有什么效果。
3. 向`build.gradle`追加如下内容：

```gradle
task runJar(type: Exec) {
    dependsOn jar
    group = "Execution"
    description = "Run the output executable jar with ExecTask"
    commandLine "java", "-jar", jar.archiveFile.get()
}
```

1. 运行`gradle runJar`



相关命令

-?, -h, --help                     Shows this help message.
-a, --no-rebuild                   Do not rebuild project dependencies.
-b, --build-file                   Specify the build file. [deprecated]
--build-cache                      Enables the Gradle build cache. Gradle will try to reuse outputs from previous builds.
-c, --settings-file                Specify the settings file. [deprecated]
--configuration-cache              Enables the configuration cache. Gradle will try to reuse the build configuration from previous builds. [incubating]
--configuration-cache-problems     Configures how the configuration cache handles problems (fail or warn). Defaults to fail. [incubating]
--configure-on-demand              Configure necessary projects only. Gradle will attempt to reduce configuration time for large multi-project builds. [incubating]
--console                          Specifies which type of console output to generate. Values are 'plain', 'auto' (default), 'rich' or 'verbose'.
--continue                         Continue task execution after a task failure.
-D, --system-prop                  Set system property of the JVM (e.g. -Dmyprop=myvalue).
-d, --debug                        Log in debug mode (includes normal stacktrace).
--daemon                           Uses the Gradle daemon to run the build. Starts the daemon if not running.
--export-keys                      Exports the public keys used for dependency verification.
-F, --dependency-verification      Configures the dependency verification mode. Values are 'strict', 'lenient' or 'off'.
--foreground                       Starts the Gradle daemon in the foreground.
-g, --gradle-user-home             Specifies the Gradle user home directory. Defaults to ~/.gradle
-I, --init-script                  Specify an initialization script.
-i, --info                         Set log level to info.
--include-build                    Include the specified build in the composite.
-M, --write-verification-metadata  Generates checksums for dependencies used in the project (comma-separated list)
-m, --dry-run                      Run the builds with all task actions disabled.
--max-workers                      Configure the number of concurrent workers Gradle is allowed to use.
--no-build-cache                   Disables the Gradle build cache.
--no-configuration-cache           Disables the configuration cache. [incubating]
--no-configure-on-demand           Disables the use of configuration on demand. [incubating]
--no-daemon                        Do not use the Gradle daemon to run the build. Useful occasionally if you have configured Gradle to always run with the daemon by default.
--no-parallel                      Disables parallel execution to build projects.
--no-scan                          Disables the creation of a build scan. For more information about build scans, please visit https://gradle.com/build-scans.
--no-watch-fs                      Disables watching the file system.
--offline                          Execute the build without accessing network resources.
-P, --project-prop                 Set project property for the build script (e.g. -Pmyprop=myvalue).
-p, --project-dir                  Specifies the start directory for Gradle. Defaults to current directory.
--parallel                         Build projects in parallel. Gradle will attempt to determine the optimal number of executor threads to use.
--priority                         Specifies the scheduling priority for the Gradle daemon and all processes launched by it. Values are 'normal' (default) or 'low'
--profile                          Profile build execution time and generates a report in the <build_dir>/reports/profile directory.
--project-cache-dir                Specify the project-specific cache directory. Defaults to .gradle in the root project directory.
-q, --quiet                        Log errors only.
--refresh-dependencies             Refresh the state of dependencies.
--refresh-keys                     Refresh the public keys used for dependency verification.
--rerun-tasks                      Ignore previously cached task results.
-S, --full-stacktrace              Print out the full (very verbose) stacktrace for all exceptions.
-s, --stacktrace                   Print out the stacktrace for all exceptions.
--scan                             Creates a build scan. Gradle will emit a warning if the build scan plugin has not been applied. (https://gradle.com/build-scans)
--status                           Shows status of running and recently stopped Gradle daemon(s).
--stop                             Stops the Gradle daemon if it is running.
-t, --continuous                   Enables continuous build. Gradle does not exit and will re-execute tasks when task file inputs change.
--update-locks                     Perform a partial update of the dependency lock, letting passed in module notations change version. [incubating]
-v, --version                      Print version info.
-w, --warn                         Set log level to warn.
--warning-mode                     Specifies which mode of warnings to generate. Values are 'all', 'fail', 'summary'(default) or 'none'
--watch-fs                         Enables watching the file system for changes, allowing data about the file system to be re-used for the next build.
--write-locks                      Persists dependency resolution for locked configurations, ignoring existing locking information if it exists
-x, --exclude-task                 Specify a task to be excluded from execution.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>
    <div class="tab">
        <div class="yab_list">
            <ul>
                <li class="current">商品介绍</li>
                <li>
                    规格与包装
                </li>
                <li>
                    售后保障
                </li>
                <li>
                    商品评价
                </li>
                <li>
                    手机社区
                </li>
            </ul>
        </div>
        <div class="tab_con">
            <div class="item" style="display:block;">商品介绍模块内容</div>
            <div class="item">规格与包装模块类容</div>
            <div class="item">售后保障模块类容</div>
            <div class="item">商品评价(5000)模块类容</div>
            <div class="item">手机模块类容</div>
        </div>
    </div>
    <title>杨攀211124010614</title>
    <script>
        var tab_list = document.querySelector('.tab_list');
        var lis = tab_list.querySelectorAll('li');
        var items = document.querySelectorAll('.item')
        for (var i=0;i < lis .length;i++){
            lis[i].setAttribute('insex',i);
            lis[i].onclick = function(){
                for(var i = 0;i< lis.length;i++){
                    lis[i].className='';
                }
                this.className = 'current'
                var index = this.getAttribute('index')
                for(var i = 0 ;i < items.length;i++){
                    items[i].style.display='none';
                }
                items[index].style.display='block';
            };
        }
    </script>
</body>
</html>
```

