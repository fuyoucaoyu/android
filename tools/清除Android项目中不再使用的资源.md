# 清除 Android 项目中不再使用的资源：
1. lint
2. android-resource-remover

## 查找无用资源 - lint：检查代码
1. 手动导出
    1. Android Studio > Gradle > Tasks > verification > lint
    2. 点击运行之后，会在目录 build/reports/ 下生成两个文件:
            lint-results.xml
            lint-results.html
    3. 文件内会有 Unused resources，列出了无用的资源文件路径、无用资源文件内容，图片或者代码会展示预览；
2. 自动导出
    1. 进入项目根目录
    2. ./gradlew clean build app:lint  或者  ./gradlew clean build :lint 
    3. 目录 build/reports/ 下生成四个文件
            lint-results.xml
            lint-results.html
            lint-results-release-fatal.html
            lint-results-release-fatal.xml
    4. 前两个文件内会有 Unused resources，列出了无用的资源文件路径、无用资源文件内容，图片或者代码会展示预览；

## 删除无用资源 - android-resource-remover
1. android-resource-remover --app src/main/ --xml ../../build/reports/lint-results.xml
2. 执行结果类似这种：removing resource: ****.png
   

注：
    1. App 目录，可以通过 --app 设置，如果未设置默认为当前目录；
    2. android-resource-remover 会去 App 目录下直接查找 AndroidManifest.xml
    3. lint-results.xml 如果是相对路径，当前目录也是 App 的目录


## android-resource-remover 安装
前置条件 Python: >= 2.7.*，不建议使用 3.0 及以上
源码：https://github.com/KeepSafe/android-resource-remover
1. 通过 pip 安装
    1. 安装 pip：
        指导：https://pip.pypa.io/en/stable/installing/
            1. curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
            2. python get-pip.py
            3. pip --version
    2. 安装 android-resource-remover
        pip install android-resource-remover
    注：pip 安装的 android-resource-remover，可能出现 android-resource-remover command not found 问题
2. 通过 easy_install 安装
    1. 安装 easy_install
        指导：https://pypi.org/project/setuptools/
            1. 下载：http://peak.telecommunity.com/dist/ez_setup.pyp
            2. 安装：python ez_setup.py
    2. 安装 android-resource-remover 
            1. 下载： android-resource-remover https://pypi.org/simple/android-resource-remover/
            2. 下载：https://github.com/KeepSafe/android-resource-remover 打包成 android-resource-remover.tar.gz
            2. 安装：easy_install android-resource-remover-0.1.7.tar.gz
    注：easy_install 安装的 android-resource-remover 版本相对较早


## Example Steps
1. cd /demoapp
2. ./gradlew clean build app:lint 
3. android-resource-remover --app app --xml build/reports/lint-results.xml
