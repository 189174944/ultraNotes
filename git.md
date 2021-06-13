```bsh
git clone --depth 1
```

总结：

用 git clone --depth=1 的好处是限制 clone 的深度，不会下载 Git 协作的历史记录，这样可以大大加快克隆的速度
depth用于指定克隆深度，为1即表示只克隆最近一次commit
适合用 git clone --depth=1 的场景：你只是想clone最新版本来使用或学习，而不是参与整个项目的开发工作

git fetch --depth 1 origin remote_branch_name $ git checkout remote_branch_name