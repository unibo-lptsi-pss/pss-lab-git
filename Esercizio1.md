# Esercizio con Git, in locale

Per ogni passo,
si annoti in questo file il comando utilizzato ed il suo output,
per confrontarlo con le soluzioni.

### Si crei una nuova directory

```
❯ mkdir deleteme
```

### Si inizializzi un repository Git dentro la cartella suddetta.

```
❯ cd deleteme
❯ git init
Initialized empty Git repository in /home/danysk/LocalProjects/exercises/deleteme/.git/
```

### Si osservi lo stato del repository

```
❯ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

### Si scriva un file `HelloWorld.java` contenente un `main` con una stampa a video e si osservi il contenuto del repository

```
git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        HelloWorld.java

nothing added to commit but untracked files present (use "git add" to track)
```

### Si aggiunga `HelloWorld.java` allo stage, e si osservi lo stato del repository

```
❯ git add HelloWorld.java
❯ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   HelloWorld.java
```

### Si crei il primo commit, con messaggio ragionevole. Se necessario, si configuri nome utente ed email di git usando i dati dell'account istituzionale.

```
❯ git commit -m 'create HelloWorld.java'
[master (root-commit) d82cd28] create HelloWorld.java
 1 file changed, 5 insertions(+)
 create mode 100644 HelloWorld.java
```

### Si compili il file Java e si verifichi lo stato del repository

```
❯ javac -d . HelloWorld.java
❯ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        HelloWorld.class

nothing added to commit but untracked files present (use "git add" to track)
```

### Si noti che c'è un file rigenerabile (`HelloWorld.class`). Si costruisca una lista di file ignorati che ignori tutti i file con estensione `.class`

```
❯ echo '*.class' >> .gitignore
❯ cat .gitignore
*.class
```

### Si osservi lo stato del repository

```
❯ git status
On branch master
Untracked files:
(use "git add <file>..." to include in what will be committed)
.gitignore

nothing added to commit but untracked files present (use "git add" to track)
```

### Si crei un nuovo commit che tracci il la ignore list, aggiungendo allo stage i file necessari. Si osservi sempre lo stato del repository dopo l'esecuzione di un comando

```
❯ git add .gitignore
❯ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   .gitignore

❯ git commit -m 'create an ignore list'
[master ad267b4] create an ignore list
 1 file changed, 1 insertion(+)
 create mode 100644 .gitignore
❯ git status
On branch master
nothing to commit, working tree clean
```

### Si gestiscano i caratteri di fine linea in modo appropriato, creando un file `.gitattributes`

```
❯ echo '* text=auto eol=lf' >> .gitattributes
❯ echo '*.[cC][mM][dD] text eol=crlf' >> .gitattributes
❯ echo '*.[bB][aA][tT] text eol=crlf' >> .gitattributes
❯ echo '*.[pP][sS]1 text eol=crlf' >> .gitattributes
❯ cat .gitattributes
* text=auto eol=lf
*.[cC][mM][dD] text eol=crlf
*.[bB][aA][tT] text eol=crlf
*.[pP][sS]1 text eol=crlf
❯ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitattributes

nothing added to commit but untracked files present (use "git add" to track)
❯ git add .gitattributes
❯ git commit -m 'create the attribute files'
[master c8fdbb3] create the attribute files
 1 file changed, 4 insertions(+)
 create mode 100644 .gitattributes
```

### Si osservi la storia del repository usando `git log --all --graph`

```
❯ git log --all --graph
* commit c8fdbb37054d2f21b12e1a4a5362ebd6f9a0e97c (HEAD -> master)
| Author: Danilo Pianini <danilo.pianini@unibo.it>
| Date:   Fri Oct 7 10:32:49 2022 +0200
| 
|     create the attribute files
| 
* commit ad267b4937245469f850185905c8104e5335078b
| Author: Danilo Pianini <danilo.pianini@unibo.it>
| Date:   Fri Oct 7 10:22:45 2022 +0200
| 
|     create an ignore list
| 
* commit d82cd28dade66d61eb06c216df0cf3b5ec23766f
  Author: Danilo Pianini <danilo.pianini@unibo.it>
  Date:   Fri Oct 7 10:12:28 2022 +0200
  
      create HelloWorld.java
```

### Da questo punto in poi, prima e dopo ogni comando, ci si assicuri di osservare lo stato del repository con `git status`

### Si crei un file Mistake.java, con contenuto arbitrario, lo si aggiunga al tracker, e si faccia un commit

```
❯ echo 'completely wrong' > Mistake.java
❯ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        Mistake.java

nothing added to commit but untracked files present (use "git add" to track)
❯ git add Mistake.java
❯ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   Mistake.java

❯ git commit -m 'add Mistake.java'
[master 777b6d5] add Mistake.java
 1 file changed, 1 insertion(+)
 create mode 100644 Mistake.java
❯ git status
On branch master
nothing to commit, working tree clean
```

### Si rinomini `Mistake.java` in `ToDelete.java`, e si faccia un commit che registra la modifica

```
❯ mv Mistake.java ToDelete.java
❯ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    Mistake.java

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        ToDelete.java

no changes added to commit (use "git add" and/or "git commit -a")
❯ git add Mistake.java ToDelete.java
❯ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    Mistake.java -> ToDelete.java

❯ git commit -m 'rename Mistake into ToDelete'
[master e8f6321] rename Mistake into ToDelete
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename Mistake.java => ToDelete.java (100%)
❯ git status
On branch master
nothing to commit, working tree clean
```

### Si elimini `ToDelete.java` e si registri la modifica in un commit

```
❯ rm ToDelete.java
❯ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    ToDelete.java

no changes added to commit (use "git add" and/or "git commit -a")
❯ git add ToDelete.java
❯ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    ToDelete.java

❯ git commit -m 'remove ToDeleTe.java'
[master dbe6d06] remove ToDeleTe.java
 1 file changed, 1 deletion(-)
 delete mode 100644 ToDelete.java
```

### Si osservi la storia del repository e si identifichi il commit dove è stato creato `Mistake.java`. Per una visione compatta, si usi l'opzione `--oneline`

```
❯ git log --all --graph --oneline
* dbe6d06 (HEAD -> master) remove ToDeleTe.java
* e8f6321 rename Mistake into ToDelete
* 777b6d5 add Mistake.java
* c8fdbb3 create the attribute files
* ad267b4 create an ignore list
* d82cd28 create HelloWorld.java
```

Nel nostro caso il commit è `777b6d5`. Si noti che gli hash possono cambiare da repository a repository.

### Si ripristini Mistake.java dal commit identificato al passo precedente

```
❯ git checkout 777b6d5 -- Mistake.java
❯ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   Mistake.java
```

Si noti che viene messo nello stage.

### Si rimuova il file ripristinato e si ripulisca lo stage

```
❯ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   Mistake.java

❯ git reset Mistake.java
❯ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        Mistake.java

nothing added to commit but untracked files present (use "git add" to track)
❯ rm Mistake.java
❯ git status
On branch master
nothing to commit, working tree clean
```

### Si torni al commit precedente a quello in cui `Mistake.java` è stato creato. Si utilizzi la storia del repository se utile.

```
❯ git log --all --graph --oneline
* dbe6d06 (HEAD -> master) remove ToDeleTe.java
* e8f6321 rename Mistake into ToDelete
* 777b6d5 add Mistake.java
* c8fdbb3 create the attribute files
* ad267b4 create an ignore list
* d82cd28 create HelloWorld.java
```

Per noi è il commit `c8fdbb3`

```
❯ git checkout c8fdbb3
Note: switching to 'c8fdbb3'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at c8fdbb3 create the attribute files
❯ git status
HEAD detached at c8fdbb3
nothing to commit, working tree clea
```

### Si crei un nuovo branch di nome `experiment` e si agganci la `HEAD` al nuovo branch

```
❯ git branch experiment
❯ git status
HEAD detached at c8fdbb3
nothing to commit, working tree clea
❯ git checkout experiment
Switched to branch 'experiment'
❯ git status
On branch experiment
nothing to commit, working tree clean
```

Alternativa valida: `git checkout -b experiment`

### Si crei un file README.md con contenuto a piacere, e si faccia un commit che lo includa

```
❯ echo 'this is a readme' >> README.md
❯ cat README.md
this is a readme
❯ git status
On branch experiment
Untracked files:
(use "git add <file>..." to include in what will be committed)
README.md

nothing added to commit but untracked files present (use "git add" to track)
❯ git add README.md
❯ git status
On branch experiment
Changes to be committed:
(use "git restore --staged <file>..." to unstage)
new file:   README.md

❯ git commit -m 'create a README file'
[experiment 901ce27] create a README file
1 file changed, 1 insertion(+)
create mode 100644 README.md
❯ git status
On branch experiment
nothing to commit, working tree clean
```

### Si torni sul branch master e si elenchino i branch disponibili

```
❯ git checkout master
Switched to branch 'master'
❯ git status
On branch master
nothing to commit, working tree clean
❯ git branch -v
experiment 901ce27 create a README file
* master     dbe6d06 remove ToDeleTe.java
```

### Si unisca il branch experiment al branch master (si faccia un merge in cui experiment viene messo dentro master, e non viceversa)

```
❯ git merge experiment
Merge made by the 'ort' strategy.
 README.md | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
❯ git status
On branch master
nothing to commit, working tree clean
```

### Si osservi la storia del repository

```
❯ git log --all --graph --oneline
*   a8cbe9c (HEAD -> master) Merge branch 'experiment'
|\  
| * 901ce27 (experiment) create a README file
* | dbe6d06 remove ToDeleTe.java
* | e8f6321 rename Mistake into ToDelete
* | 777b6d5 add Mistake.java
|/
* c8fdbb3 create the attribute files
* ad267b4 create an ignore list
* d82cd28 create HelloWorld.java
```
