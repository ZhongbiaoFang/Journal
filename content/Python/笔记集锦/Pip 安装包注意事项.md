![image.png](https://elvisfang.oss-cn-hangzhou.aliyuncs.com/img/202506051936693.png)

### 查看已安装软件包版本
![image.png](https://elvisfang.oss-cn-hangzhou.aliyuncs.com/img/202506051937125.png)

从报错信息来看，这是由于 SSL 证书验证失败导致 `pip` 无法从官方源下载 `jupyter` 安装包。以下是几种不同的解决方法，你可以依次尝试：
### 方法一：使用国内镜像源安装<u>（推荐）</u>（类似于装 R 包）
国内的一些镜像源（如清华大学开源软件镜像站、阿里云镜像等）通常可以更稳定地获取安装包，并且可能不存在证书验证问题。
![image.png](https://elvisfang.oss-cn-hangzhou.aliyuncs.com/img/202506061330350.png)

以清华大学开源软件镜像站为例，使用以下命令安装 `jupyter`：
```bash
pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple jupyter
```
你也可以尝试阿里云镜像：
```bash
pip3 install -i https://mirrors.aliyun.com/pypi/simple/ jupyter
```

==当然，也可以直接在 Pycharm 自身的软件包界面搜索并安装需要的库==
![image.png](https://elvisfang.oss-cn-hangzhou.aliyuncs.com/img/202506061442014.png)




---
### 方法二：更新证书相关包
尝试更新 `certifi` 包（该包包含了许多根证书），在终端（先激活虚拟环境）执行：
```bash
pip3 install --upgrade certifi
```
安装完成后，再次尝试安装 `jupyter`：
```bash
pip3 install jupyter
```

### 方法三：配置 pip 信任官方源（不推荐长期使用，但可临时解决）
在终端执行以下命令（先激活虚拟环境），临时让 `pip` 信任 `pypi.org` 和 `files.pythonhosted.org`：
```bash
pip3 install jupyter --trusted-host pypi.org --trusted-host files.pythonhosted.org
```
这种方式是跳过了 SSL 证书验证，存在一定安全风险，不建议在生产环境或长期使用场景中采用。

### 方法四：检查系统代理设置（如果使用了代理）
如果你的网络环境配置了代理服务器，可能会影响 SSL 证书验证。
1. 查看当前代理环境变量：
```bash
echo $HTTP_PROXY
echo $HTTPS_PROXY
```
如果有输出值（即设置了代理），尝试临时取消代理（执行以下命令）后再安装：
```bash
unset HTTP_PROXY
unset HTTPS_PROXY
pip3 install jupyter
```
如果取消代理后能成功安装，说明代理配置可能存在问题，你需要进一步排查代理服务器的 SSL 证书相关配置（这部分操作较复杂，不同代理软件配置方式不同，你可查阅对应代理软件的文档）。

### 方法五：修复系统证书存储（适用于 macOS）
在 macOS 上，可以尝试通过以下步骤修复证书存储：
1. 打开 “钥匙串访问” 应用（在 `“应用程序” -> “实用工具”` 中）。
2. 在左侧栏选择 “系统” 钥匙串，然后在菜单中选择 `“钥匙串急救”`（位于 `“钥匙串访问” -> “设置” -> “证书”` 相关路径，具体可能因系统版本略有不同）。
3. 按照提示操作，尝试修复证书存储。完成后，再次尝试安装 `jupyter`。

通过以上几种方法的尝试，一般可以解决 SSL 证书验证失败导致的安装问题。如果还有其他报错或问题，请随时告知。