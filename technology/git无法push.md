# git push 报错
```
kex_exchange_identification: Connection closed by remote host
Connection closed by 198.18.0.32 port 22
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
```
首先能比较直观的推测可能是梯子或者clash本身的问题。因此排查方向需要往网络问题方面研究。
由于是使用ssh连接github，所以有如下的搜索
- https://stackoverflow.com/questions/6178401/how-can-i-debug-git-git-shell-related-problems
- 大概意思是想办法打印更多的debug日志
- ssh -vvvT git@github.com，这个命令是关键，基本上可以知道是ssh的问题
- https://docs.github.com/zh/authentication/troubleshooting-ssh/using-ssh-over-the-https-port
- http://www.inanzzz.com/index.php/post/wa1f/solution-for-ssh-connect-to-host-github-com-port-22-connection-timed-out-error
- 这两个link。描述了问题的根源

# 修复
```
$ sudo nano ~/.ssh/config
 
# Add section below to it
Host github.com
  Hostname ssh.github.com
  Port 443
```
