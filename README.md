# AlistWebDAV
主页市场OSS-自动化部署参考文件

# 基于Github Actions的Github Alist同步方法

配置

库 创建.github/workflows文件夹

在 Settings/Secrets/Actions/Repository secrets 配置以下内容

${{ secrets.WEBDAV_HOST }} OSS域名

${{ secrets.WEBDAV_PORT }} OSS端口

${{ secrets.ALIST_USERNAME }}  OSSID

${{ secrets.ALIST_PASSWORD }}  OSS密码

需要联系 @JingHai-Lingyun 或 @Joker2184 开通 OSS Webdav 使用（默认不开通）

