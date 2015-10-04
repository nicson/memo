# git よく使うコマンドまとめa
 [GitHub Markdown](https://guides.github.com/features/mastering-markdown/)  
たまに使いたくなる使い方を検索する手間を省くためにメモ  

## 修正内容の破棄

### 1. 修正内容を破棄(未コミット内容)
修正内容を全て消したい、前回のコミット時の状態にしたい時つかう
2通りあり、１つめは
>git checkout .

たまにこれでうまくいかないときがあるので、その場合は以下を使用し強制的にリセットする  
__※注　マジで戻せないのでミスタイプに注意__
>git reset --hard HEAD

### 2. 直前コミットを破棄
前々回のコミット直後の内容になる
>git reset --hard HEAD^

### 3. 直前のコミットを破棄するけど変更はそのままで
直前のコミットは破棄するが、今の編集状態はそのままにしたい時、
hard->softにする
>git reset --soft HEAD^


### 4. ファイル単位で修正内容を破棄(未コミット内容)
resetコマンドでの修正破棄はコミット単位でしたが、ファイル単位の修正破棄がcheckoutで可能です
>git checkout -- filePath

### 5. 前回のコミット内容を打ち消すコミット
revertコマンドでは、コミット内容を打ち消すコミットをすることができ、
修正内容を消した履歴を残したいときにつかう。まどろっこしくなるので使わないと思う
>git revert HEAD

## コミットをまとめる

### 1. 過去３回分のコミットを１つにまとめる


過去のコミットをまとめるには、rebase -iを使います。
>$ git rebase -i HEAD~3

テキストエディタが開いて、HEADからHEAD~3までの過去３回分のコミットが次のように表示されます。


```
pick 2f56e41 1time
pick bfeba86 2time
pick 25acaf6 3time

# Rebase f0ef38f..25acaf6 onto f0ef38f (3 command(s))
# ...省略...
#
# Note that empty commits are commented out
```

2,3行目のpickをsquashに変えて保存。  
これで、2,3行目のコミットが１行目のコミットにメルトインされ、コミットコメントを編集できる
(1行目はsquashに変えられない)

```
pick 2f56e41 1time
squash bfeba86 2time
squash 25acaf6 3time
```

またエディタが開く。過去３回分のコミットのコメントが表示される。

```
# This is a combination of 3 commits.
# The first commit's message is:
1time

# This is the 2nd commit message:

2time

# This is the 3rd commit message:

3time

# Please enter the commit message for your changes. Lines starting
# ...略
# Changes to be committed:
#   modified:   atom.txt
```

３回分のコメントを全て消し、新たなコメントを入力し、保存で完了

```
new commit

# Please enter the commit message for your changes. Lines starting  
# ...省略...
# Changes to be committed:
#   modified:   atom.txt
```
