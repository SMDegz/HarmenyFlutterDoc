# 鸿蒙应用如何集成Flutter模块

## 1. 前置条件

- 完成 [Flutter OH 环境搭建](https://gitcode.com/openharmony-tpc/flutter_samples/blob/master/ohos/docs/03_environment/openHarmony-flutter%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E6%8C%87%E5%AF%BC.md)
- 已安装 [DevEco Studio](https://developer.huawei.com/consumer/cn/deveco-studio/) 工具

## 2. 创建鸿蒙项目

1. 打开 `DevEco Studio`，选择 `File -> New -> Create Project` 创建项目。

2. 项目创建完成，查看目录结构，以下几个文件与集成Flutter相关：

   ```json
   Project/
   ├─ oh-package.json5              # 项目依赖配置
   ├─ entry/                        # 主模块目录
   │  ├─ oh-package.json5           # 主模块依赖配置
   │  └─ src/
   │     ├─ main/
   │     │  ├─ ets/
   │     │  │  ├─ entryability/
   │     │  │  │  └─ EntryAbility.ets      # 主模块Ability
   │     │  │  └─ pages/
   │     │  │     └─ Index.ets             # 页面代码
   │     │  └─ resources/
   │     │     ├─ base/
   │     │     │  └─ profile/
   │     │     │     └─ main_pages.json    # 页面配置
   ```

## 4.集成Flutter

### 4.1 创建Flutter模块

在项目根目录下执行：

```bash
flutter create -t module flutter_module
```

生成 `flutter_module` 模块

### 4.2 构建Flutter模块

进入 `flutter_module` 目录，执行：

```bash
flutter build har --debug  # --[debug,--release]
```

执行完成，打开`Project/flutter_module/build/ohos/har/` 目录：

```json
debug/
|--arm64_v8a_debug.har
|--flutter_embedding_debug.har
|--flutter_module.har
```

生成3个har文件，即构建成功。

### 4.3 配置Flutter模块

1. 修改主项目 `oh-package.json5`

   打开项目`Project/oh-package.json5`文件，在 `"overrides"`节点添加如下内容（路径需替换为实际HAR包路径）：

   ```json
   "overrides": {
      "@ohos/flutter_ohos": "file:./har/flutter_embedding_debug.har",
      "flutter_native_arm64_v8a": "file:./har/arm64_v8a_debug.har",
      "@ohos/flutter_module": "file:./har/flutter_module.har"
   }
   ```

2. 修改 `Project/entry/oh-package.json5`

   打开 `Project/entry/oh-package.json`，在 `"dependencies"` 节点添加如下内容：

   ```json
   "dependencies": {
      "@ohos/flutter_ohos": "",
      "flutter_native_arm64_v8a": "",
      "@ohos/flutter_module": ""
   }
   ```

3. 执行 `Sync Now` 或 `ohpm install` 

   执行完成，查看 `Project/entry` 目录：

   ```json
   Project/
   ├─ entry/                       
   │  ├─ oh_modules   # 依赖包缓存
   ```

   `oh_modules` 目录生成，集成完成。

## 5. 加载显示Flutter

**完成Flutter模块集成之后，就可以显示Flutter相关页面**

1. 鸿蒙Ability生命周期与Flutter模块集成

   ```js
   export default class EntryAbility extends UIAbility {
   
     detachFromFlutterEngine(): void {
     }
   
     getAppComponent(): UIAbility {
       return this;
     }
   
     onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
       FlutterManager.getInstance().pushUIAbility(this);
     }
   
     onDestroy(): void | Promise<void> {
       FlutterManager.getInstance().popUIAbility(this);
     }
   
     onWindowStageCreate(windowStage: window.WindowStage): void {
       windowStage.getMainWindowSync().setWindowLayoutFullScreen(true);
       FlutterManager.getInstance().pushWindowStage(this, windowStage);
       windowStage.loadContent('pages/Index');
     }
   
     onWindowStageDestroy() {
       FlutterManager.getInstance().popWindowStage(this);
     }
   }
   ```

2. 实现FlutterEntry类

   ```js
   export default class MyFlutterEntry extends FlutterEntry {
     configureFlutterEngine(flutterEngine: FlutterEngine): void {
       super.configureFlutterEngine(flutterEngine);
       GeneratedPluginRegistrant.registerWith(flutterEngine);
   
       // 在这里注册需要使用的插件
       this.delegate?.addPlugin(new CustomPlugin());
     }
   }
   ```

3. 新建一个Page页，用于显示Flutter页面

   ```js
   @Entry
   @Component
   struct FlutterIndex {
     private flutterEntry: FlutterEntry | null = null;
     private flutterView?: FlutterView
   
     aboutToAppear() {
       this.flutterEntry = new MyFlutterEntry(getContext(this))
       this.flutterEntry.aboutToAppear()
       this.flutterView = this.flutterEntry.getFlutterView()
     }
   
     aboutToDisappear() {
       this.flutterEntry?.aboutToDisappear()
     }
   
     onPageShow() {
       this.flutterEntry?.onPageShow()
     }
   
     onPageHide() {
       this.flutterEntry?.onPageHide()
     }
   
     build() {
       Stack() {
         FlutterPage({ viewId: this.flutterView?.getId() })
       }
     }
   
     onBackPress(): boolean {
       this.flutterEntry?.onBackPress();
       return true
     }
   }
   ```

4. 打开 `Project/entry/src/main/resources/base/profile/main_pages.json` 文件，配置新增 `Page`:

   ```json
   {
     "src": [
       "pages/Index",
       "pages/FlutterIndex"
     ]
   }
   ```

5. 路由打开Flutter页面

   ```js
   Button('打开 Flutter 页面')
   	.onClick(() => {
   		router.push({
   			url: 'pages/FlutterIndex',
   		})
   	});
   ```

## 6. FAQ

- 集成 `flutter_module` 后，`entry`  里没有生成 `oh_modules` 缓存目录。

  需要在项目根路径下执行 `ohpm install`，不是在 `entry` 下执行。



- 修改了 `flutter_modules` 里的代码，没有生效。

  修改 `flutter_modules` 里的业务代码之后，需要在 `flutter_modules` 目录下执行 `flutter build har --[debug, release]` 命令，用于更新har包。
