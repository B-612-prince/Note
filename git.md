# 问题一
代码在本地修改之后丢失：
1. 已经提交到远程
```bash
git add .
git commit -m "一次提交"
git push
```
Wolves项目在周五提交之后，周一来上班发现自己的本地代码全部回退到修改之前的状态了，但是因为直接`push`到远程了，于是直接`pull`到本地来了

2. 仅仅在本地暂存
```bash
git add .
git stash
```

chatbot-admin项目在周五暂存之后，周一发现本地代码无了，通过`git reflog`查看了提交记录，确定我没有在add之后使用commit，`git stash list`查看stash记录（但是我当时没有看懂stash记录的形式，误以为自己没有存上

代码看起来无了/git stash list没有想要的内容有两种可能：

- 在`git add .`之后执行了`git commit ···`，此时工作区与暂存区就都是干净的，再执行`git stash`，不会保存任何东西。
- 在`git stash`之后，修改的内容就会被存在暂存区，代码会回退到修改之前的状态，看起来就好像没有改一样

如果stash成功了，可以通过stash pop 将最近的一次stash恢复

我当时是通过时间线中的文件内容复制粘贴恢复文件的。

# 问题二
git commit -m "……" 汉字内容会被吞，然后外补一个引号
> 比如：原本想要的是：git commit -m "enhancement:充值页面修改"，变成了git commit -m "enhancement:值页面修改""

chatGPT给的答案是：

## ✅ 本质原因：

这是 **终端字符编码或字体兼容性异常** + **特殊字符导致命令解析异常** 的组合问题，尤其发生在：

| 环境                       | 常见问题                  |
| ------------------------ | --------------------- |
| Windows（cmd、PowerShell）  | 中文字符（尤其“充”这种多字节）被错误拆分 |
| 使用非 UTF-8 编码终端           | 部分字符被截断或乱码            |
| VSCode Terminal（Windows） | 字符渲染/剪贴板交互异常，出现“补双引号” |

---

## 💥 问题分析：

1. `"充"` 是一个 **多字节 UTF-8 字符**，有些终端无法正确处理它；
2. 输入命令时，剪贴板或输入法可能引入 **隐形控制符**（比如 Unicode 零宽空格）；
3. Git Bash / VSCode Terminal / Windows Terminal 在解释参数时，把这些字符误当成命令终止标记，就导致：

   * “吞字” ➜ 中间字符被截断；
   * “补引号” ➜ Git Shell 认为你命令没闭合，引号自动补了一个。

---

## ✅ 解决方案合集

### ✅ 推荐方式：**直接用英文命令行 + UTF-8 终端 + 手打引号**

你可以这样做：

```bash
git commit -m "enhancement: 充值页面修改"
```

确保不是粘贴的内容里带了 **奇怪的空格/换行符** 或其他控制字符。

---

### ✅ 方法一：使用 Git Bash（确保语言是 UTF-8）

打开 Git Bash，输入命令前执行：

```bash
export LANG=en_US.UTF-8
```

然后再运行：

```bash
git commit -m "enhancement: 充值页面修改"
```

---

### ✅ 方法二：避免使用 `"中文"` 包裹在英文前面，改为：

```bash
git commit -m "充值页面修改：优化充值流程"
```

有时冒号 + 中文容易出 bug，你可以先测试把冒号挪到后面或干脆不用冒号。

---

### ✅ 方法三：使用 `--file` 临时写入 commit 信息文件

```bash
echo "enhancement: 充值页面修改" > commit-msg.txt
git commit -F commit-msg.txt
```

这样就**完全避开终端输入问题**，是最稳妥的方法。

---

## ✅ 总结

| 方法                 | 描述                                               |
| ------------------ | ------------------------------------------------ |
| 🔧 设置终端 UTF-8      | Windows 使用 `chcp 65001`，Git Bash 设置 `LANG=utf-8` |
| 🧹 避免粘贴含控制字符       | 尽量手敲命令内容                                         |
| 💡 避免用中文字符夹在英文冒号后面 | 可以先写中文、或冒号放后面                                    |
| 📝 用 `-F` 提交文件方式   | 规避所有终端编码/字符问题                                    |

---

它库库输出，但是我发现电脑系统更新之后就好了（不确定和电脑系统更新有没有关系，反正现在又好了

# 问题三

明明已经挂了梯子，但是git push或者使用cursor的源代码管理同步提交都报错链接超时，这个是因为git没有走代理，相当于git没用上vpn，对git进行一下网络代理配置就行
```bash
#Git配置代理
git config --global http.proxy socks5h://127.0.0.1:10808
git config --global https.proxy socks5h://127.0.0.1:10808
#验证配置是否生效
git ls-remote https://github.com/github/gitignore.git
#返回一堆类似与以下内容说明git已经走代理了
#d3b4ccf.... refs/heads/main

# 还原代理（公司项目用不了梯子，所以要清理配置
git config --global --unset http.proxy
git config --global --unset https.proxy
```

