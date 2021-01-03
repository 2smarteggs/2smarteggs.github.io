# Git批量修改commit作者与邮箱

### 1. 创建一个.sh文件并在其中添加如下shell代码

将```original@original.com```更改为所要修改的邮箱，将```modify```和```modify@modify.com```更改为要修改成的名称和邮箱

```shell
#!/bin/sh

git filter-branch -f --env-filter '

an="$GIT_AUTHOR_NAME"
am="$GIT_AUTHOR_EMAIL"
cn="$GIT_COMMITTER_NAME"
cm="$GIT_COMMITTER_EMAIL"

if [ "$GIT_COMMITTER_EMAIL" = "original@original.com" ]
then
    cn="modify"
    cm="modify@modify.com"
fi
if [ "$GIT_AUTHOR_EMAIL" = "original@original.com" ]
then
    an="modify"
    am="modify@modify.com"
fi

export GIT_AUTHOR_NAME="$an"
export GIT_AUTHOR_EMAIL="$am"
export GIT_COMMITTER_NAME="$cn"
export GIT_COMMITTER_EMAIL="$cm"
'
```

#### 2. 将该.sh文件拖入本地git仓库内并用命令行cd到该目录下

命令行运行```sh xxx.sh```后，所有```original@original.com```的commit作者便会变更为```modify```和```modify@modify.com```

#### 3. 在命令行运行完毕后

先直接```git push 所在分支```一次，再```git pull```一次，更改变成功提交了。该方法不会修改原先的commit时间、信息等其他内容，仅仅会对commit的作者和邮箱进行修改