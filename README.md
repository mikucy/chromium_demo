# Demo

这个项目用来演示如何使用chromium中的一些基础机制，包括异步多任务，mojo，多进程等。

> 提示：如果你是 chromium 的新手，建议按照顺序学习这些demo。

Demo 列表：

1. `demo`: 最简单的 demo，演示在自己的程序中使用 base 库；
1. `demo_log`: 演示使用日志库；
1. `demo_tasks`: 演示使用线程池 TaskScheduler;
1. `demo_messageloop`: 演示使用消息循环 MessageLoop;
1. `demo_mojo_single_process`: 演示在单进程中使用 `mojo` 库；
1. `demo_mojo_multiple_process`: 演示在多进程中使用 `mojo` 库；
1. `demo_mojo_multiple_process_binding`: 演示在多进程中使用 `mojo` 库的binding层；
1. `demo_services`: 演示使用基于 `mojo` 的 servcies 及多进程架构；
1. `demo_ipc`: 演示使用基于 `mojo` 的 IPC 接口；

更多文档见 [docs](./docs) 目录。

## 用法一(推荐)

1. 进入 chromium 的 `src` 目录；
2. 执行以下命令将该仓库clone到 `src/demo` 目录下；

    ```sh
    git clone git@gitlab.gz.cvte.cn:CrOS/seewo/demo.git demo
    ```

3. 找到你的编译输出目录中的 `out/Default/args.gn` 文件，添加以下参数：

    ```python
    # add extra deps to gn root
    root_extra_deps = ["//demo"]
    ```

4. 执行 `ninja -C out/Default demo:all` 生成所有 demo 程序（详见 [BUILD.gn](./BUILD.gn)）；

## 用法二(使用gclient)

1. 进入chromium项目的根目录（src上一层目录）找到 `.gclient` 文件；
2. 打开 `.gclient` 文件，参照下面的设置进行修改：

    ```python
    solutions = [
        { "name"        : "src",
            "url"         : "git@gitlab.gz.cvte.cn:CrOS/src.git",
            "deps_file"   : "DEPS",
            "managed"     : False,
            "custom_deps" : {
                # let gclient pull demo project to 'src/demo' dir
                "src/demo": "git@gitlab.gz.cvte.cn:CrOS/seewo/demo.git",
            },
            "custom_vars": {},
        }
    ]
    ...
    ```

3. 找到你的编译输出目录中的 `out/Default/args.gn` 文件，添加以下参数：

    ```python
    # add extra deps to gn root
    root_extra_deps = ["//demo"]
    ```

4. 执行 `gclient sync` 同步代码，这会拉取 `demo` 仓库到 `src/demo` ；
5. 执行 `ninja -C out/Default demo:all` 生成所有 demo 程序（详见 [BUILD.gn](./BUILD.gn)）；