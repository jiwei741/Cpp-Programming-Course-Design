# Git Push Verification

这个文件用于验证本机 Git 环境修复后的 **clone → commit（SSH 签名）→ push** 全链路是否正常。

## 背景

修复前本机 Git 存在以下问题：

| 问题 | 现象 |
| --- | --- |
| `git-remote-https.exe` 因 DLL 冲突崩溃 | 所有 HTTPS 操作瞬间失败（exit 3328，无任何输出） |
| `http.proxy` / `https.proxy` 指向 7890 | 该端口无监听，代理链路是死的 |
| `user.signingkey` 是未填写的占位符 | `commit.gpgsign = true` 导致每次提交都失败 |
| `gpg.ssh.program` 指向另一套 msys 的 ssh-keygen | `/tmp` 根目录不一致，签名时报找不到临时文件 |
| 缺少 GitHub 凭据助手 | HTTPS push 拿不到 token |

## 验证结果

- 克隆仓库：成功
- 提交签名：成功（SSH / ED25519）
- 推送到远程：成功

## 删除方式

如果不再需要这个文件：

```sh
git rm DSH-PUSH-VERIFY.md
git commit -m "Remove push verification file"
git push
```
