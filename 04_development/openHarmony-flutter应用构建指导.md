# OpenHarmony版Flutter应用构建指导

  1. 运行 `flutter doctor -v` 检查环境变量配置是否正确，**Flutter** 与 **HarmonyOS toolchain** 应都为`[√]`标识。若提示`[!]`，根据提示配置相应环境即可。  

  2. 创建应用

     ```bash
     # 创建应用
     flutter create --platforms ohos <projectName>
     ```

  3. 进行签名，使用 `DevEco Studio` 工具打开  `<projectName>/ohos` 项目，点击右上角 `Project Structure -> Signing Configs` 签名。

  4. 编译应用，编译产物在`/<projectName>/ohos/entry/build/default/outputs/default/entry-default-signed.hap`目录下。

     ```bash
     # 进入工程根目录编译
     # 示例：flutter build hap [--target-platform ohos-arm64] [--local-engine=<DIR>/src/out/ohos_release_arm64] --release
     flutter build hap --target-platform ohos-arm64 --<debug|release|profile> [--local-engine=src/out/<engine产物目录> --local-engine-host=src/out/<engine host目录>/]
     ```

     - 创建工程并打开impeller开关
       当前Flutter ohos平台中支持impeller-vulkan渲染模式，可通过开关控制是否打开。
       开关位于`buildinfo.json5`文件中，如果选择关闭impeller渲染，可将json文件中的value改为false。下一次运行时即可关闭。
       文件路径：`ohos/entry/src/main/resources/rawfile/buildinfo.json5`
       （初次flutter create之后，配置文件位于profile目录，首次run或build之后会搬移到rawfile目录）

       文件内容：

       ```
       {
          "string": [
             {
                "name": "enable_impeller",
                "value": "true"
             }
          ]
       }
       ```

       新建工程默认打开impeller选项。
       对于旧工程，可将以上buildinfo.json5文件复制到工程目录的对应路径下(rawfile目录)，并修改value值即可实现开关功能。如果不添加开关，则默认打开enable-impelle

  5. 通过`flutter devices`指令发现ohos设备之后，使用 `hdc -t <deviceId> install <hap file path>`进行安装。

  6. 也可直接使用下列指令运行：

     ```bash
     flutter run --debug [--local-engine=<DIR>/src/out/ohos_debug_unopt_arm64] [--local-engine-host=<DIR>/src/out/host_debug_unopt] -d <device-id>
     ```

  7. 构建hap包命令：

     ```bash
      # 示例：flutter build app --release [--local-engine=<DIR>/src/out/ohos_release_arm64] [--local-engine-host=<DIR>/src/out/host_release]
      flutter build hap --release
     ```
