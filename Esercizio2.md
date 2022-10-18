# Esercizio di risoluzione di un merge conflict

**Il tempo massimo in laboratorio per questo esercizio è di _20 minuti_.
Se superato, sospendere l'esercizio e riprenderlo per ultimo!**

Si visiti https://github.com/APICe-at-DISI/OOP-git-merge-conflict-test.
Questo repository contiene due branch: `master` e `feature`

Per ognuna delle seguenti istruzioni, si annoti l'output ottenuto.
Prima di eseguire ogni operazione sul worktree o sul repository,
si verifichi lo stato del repository con `git status`.

1. Si cloni localmente il repository

```shell
❯ git clone git@github.com:APICe-at-DISI/OOP-git-merge-conflict-test.git
Cloning into 'OOP-git-merge-conflict-test'...
X11 forwarding request failed on channel 0
remote: Enumerating objects: 12, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (3/3), done.
Receiving objects: 100% (12/12), done.
Resolving deltas: 100% (2/2), done.
remote: Total 12 (delta 1), reused 1 (delta 1), pack-reused 8
❯ cd OOP-git-merge-conflict-test
❯ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```

2. Ci si assicuri di avere localmente entrambi i branch remoti

```shell
❯ git branch -v
* master 8e0f29c Change HelloWorld to print the number of available processors
❯ git checkout -b feature origin/feature
branch 'feature' set up to track 'origin/feature'.
Switched to a new branch 'feature'
❯ git branch -v
* feature bed943f Print author information master 8e0f29c Change HelloWorld to print the number of available processors
```

3. Si faccia il merge di `feature` dentro `master`, ossia: si posizioni la `HEAD` su `master`
   e da qui si esegua il merge di `feature`

```shell
❯ git status
On branch feature
Your branch is up to date with 'origin/feature'.

nothing to commit, working tree clean
❯ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
❯ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
❯ git merge feature
Auto-merging HelloWorld.java
CONFLICT (content): Merge conflict in HelloWorld.java
Automatic merge failed; fix conflicts and then commit the result.
```

4. Si noti che viene generato un **merge conflict**!
5. Si risolva il merge conflict come segue:
   - Il programma Java risultante deve stampare sia il numero di processori disponibili
     (funzionalità presente su `master`)
     che il nome dell'autore del file
     (funzionalità presente su `feature`)

```shell
❯ cat HelloWorld.java
public final class HelloWorld {

        private static final String AUTHOR = "Danilo Pianini";

        public static void main(final String[] args) {
                System.out.println("This program has been realised by " + AUTHOR);
                System.out.println("This program is running in a PC with " + procNumber() + " logic processors!");
        }

        public static int procNumber() {
                return Runtime.getRuntime().availableProcessors();
        }

}
❯ javac HelloWorld.java
❯ java HelloWorld
This program has been realised by Danilo Pianini
This program is running in a PC with 12 logic processors!
❯ git add HelloWorld.java
❯ git commit --no-edit
[master cd50814] Merge branch 'feature'
❯ git log --all --graph --oneline
*   cd50814 (HEAD -> master) Merge branch 'feature'
|\  
| * bed943f (origin/feature, feature) Print author information
* | 8e0f29c (origin/master, origin/HEAD) Change HelloWorld to print the number of available processors
|/  
* d956df6 Create .gitignore
* 700ee0b Create HelloWorld
```

6. Si crei un nuovo repository nel proprio github personale
7. Si aggiunga il nuovo repository creato come **remote** e si elenchino i remote

```shell
❯ git remote add mine git@github.com:DanySK/merge-test.git
❯ git remote -v
mine    git@github.com:DanySK/merge-test.git (fetch)
mine    git@github.com:DanySK/merge-test.git (push)
origin  git@github.com:APICe-at-DISI/OOP-git-merge-conflict-test.git (fetch)
origin  git@github.com:APICe-at-DISI/OOP-git-merge-conflict-test.git (push)
```

8. Si faccia push del branch `master` sul proprio repository

```shell
❯ git push mine master
X11 forwarding request failed on channel 0
Enumerating objects: 15, done.
Counting objects: 100% (15/15), done.
Delta compression using up to 12 threads
Compressing objects: 100% (11/11), done.
Writing objects: 100% (15/15), 1.76 KiB | 1.76 MiB/s, done.
Total 15 (delta 4), reused 10 (delta 2), pack-reused 0
remote: Resolving deltas: 100% (4/4), done.
To github.com:DanySK/merge-test.git
 * [new branch]      master -> master
```

Soluzione alternativa (che risolve anche il punto 9):
```shell
❯ git push -u mine master
X11 forwarding request failed on channel 0
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 12 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 930 bytes | 930.00 KiB/s, done.
Total 6 (delta 2), reused 1 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 1 local object.
To github.com:DanySK/merge-test.git
   8e0f29c..cd50814  master -> master
branch 'master' set up to track 'mine/master'.
```

9. Si setti il branch remoto `master` del nuovo repository come *upstream* per il proprio branch `master` locale

```shell
❯ git branch --set-upstream-to=mine/master
branch 'master' set up to track 'mine/master'.
```
