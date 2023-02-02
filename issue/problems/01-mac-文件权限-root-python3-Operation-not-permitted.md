<!--ts-->
   * [问题 1.Operation not permitted](#问题-1operation-not-permitted)
      * [问题](#问题)
      * [原因](#原因)
      * [解决](#解决)
      * [注意事项.建议开启 SIP](#注意事项建议开启-sip)
   * [问题 2.Read-only file system](#问题-2read-only-file-system)
      * [问题](#问题-1)
      * [解决](#解决-1)

<!-- Added by: edy, at: 2022年 2月14日 星期一 13时55分45秒 CST -->

<!--te-->

# 问题 1.Operation not permitted

## 问题

1. 对于/usr/bin 目录即使切 root 也无法操作文件。

```bash
# edy@edydeMacBook-Pro bin % cd /usr/bin
# edy@edydeMacBook-Pro bin % sudo mv python3 python3-old
Password:
mv: rename python3 to python3-old: Operation not permitted
# edy@edydeMacBook-Pro bin % sudo rm -rf python3
rm: python3: Operation not permitted
# edy@edydeMacBook-Pro bin % chmod 777 /usr/bin
chmod: Unable to change file mode on /usr/bin: Operation not permitted
```

## 原因

这是因为一些 mac 用户在升级系统之后，电脑启用了 SIP（System Integrity Protection），增加了 rootless 机制，导致即使在 root 权限下依然无法修改文件，在必要时候为了能够修改下面的文件，我们只能关闭该保护机制。

SIP 的基本目的就是为了防止程序获取 root 权限，对几个系统关键目录做出修改。确实能够起到一定的保护作用。被保护的主要目录有：

```bash
# /System
# /usr
# /bin
# /sbin 以及预安装的app（比如Appstore，iTunes等等）
```

## 解决

拿回权限，关闭内核里面的 SIP，也就是 System Integrity Protection 的服务；

1. 确认下 mac 系统目前是不是开启着 SIP

```bash
# 在正常模式下，输入 csrutil status 命令，查看mac安全机制是否开启。

# edy@edydeMacBook-Pro ~ % csrutil status
System Integrity Protection status: enabled.
```

2. 确实开启 SIP 了`enabled`，则要进入安全模式进行关闭 SIP。

3. 进行安全模式操作：

```
点击屏幕左上角苹果图标，点击重新启动按钮，屏幕暗下后立马按住command + R键，直到出现屏幕中央出现苹果图标停手。
```

4. 进入安全模式界面后，先会提醒设置语言`我没设置这里，最顶上一排就能看到实用工具了`，然后会看到安全界面操作，屏幕最上面一排，找到实用工具菜单，再在里面找到终端，点击进入终端。

5. 关闭 SIP 操作，终端输入 `csrutil disable` 回车后会出现一串英文，大致意思是安全模式已经关闭，重启后生效进行操作。

6. 重启电脑，选择左上角图标 -> 重新启动，或者直接在终端输入 `reboot` 重启电脑即可。

7. 重启电脑后，在 terminal 终端中输入 `csrutil status` 会看到 `Protection status：disable`，意思是安全模式的状态：是关闭的。

到此关闭 SIP 完毕了。

## 注意事项.建议开启 SIP

SIP 保护机制还是很有用的，防止下载乱七八糟的程序后，恶意修改我们自己的电脑的重要文件，所以，不再需要修改哪些保护的目录文件后，将 SIP 开启。

开启 SIP

```bash
# 恢复SIP保护机制，重启电脑 -> command+R 和上边一样操作进入保护模式
# 输入 csrutil enable
# 然后 重启电脑 就生效了
# 查看是否SIP生效
# edy@edydeMacBook-Pro ~ % csrutil status
System Integrity Protection status: enabled.
```

# 问题 2.Read-only file system

## 问题

发现出现了新的问题：`Read-only file system`。

```bash
# edy@edydeMacBook-Pro bin % ls -rtla | grep python3
-rwxr-xr-x     1 root   wheel     31488  8 11  2020 python3
# edy@edydeMacBook-Pro bin % sudo chmod -R 777 python3
chmod: Unable to change file mode on python3: Read-only file system
```

## 解决

将根目录变为可读写的（重启后失效），执行：`sudo mount -uw /`。

```bash
# edy@edydeMacBook-Pro bin % sudo mount -uw /
# edy@edydeMacBook-Pro bin % sudo mv python3 python3-old
# edy@edydeMacBook-Pro bin % ls -rtli | grep python3
1152921500311879999 -rwxr-xr-x   1 root   wheel     31488  8 11  2020 python3-old
```
