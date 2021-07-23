## 3 Branches no Git

### 3.1 Branches em Poucas Palavras

```bash
$ git add README test.rb LICENSE
$ git commit -m 'The initial commit of my project'
```

|       ![](commit-and-tree.png)       |
| :----------------------------------: |
| **Figura 9. Um commit e sua árvore** |

|    ![](commits-and-parents.png)    |
| :--------------------------------: |
| **Figura 10. Commits e seus pais** |

|             ![](branch-and-history.png)             |
| :-------------------------------------------------: |
| **Figura 11. Um branch e seu histórico de commits** |

#### Criando um Novo Branch

```bash
$ git branch testing
```

| ![](two-branches.png)                                        |
| ------------------------------------------------------------ |
| **Figura 12. Duas branches apontando para o mesmo histórico de commits** |

| ![](head-to-master.png)                      |
| -------------------------------------------- |
| **Figure 13. HEAD apontando para um branch** |

```bash
$ git log --oneline
f30ab (HEAD -> master, testing) add feature #32 - ability to add new formats to the central interface
34ac2 Fixed bug #1328 - stack overflow under certain conditions
98ca9 The initial commit of my project
```

#### Alternando entre Branches

```bash
$ git checkout testing
```

|            ![](head-to-testing.png)            |
| :--------------------------------------------: |
| **Figura 14. HEAD aponta para o branch atual** |

```bash
$ code test.rb
$ git commit -a -m 'made a change'
```

|                   ![](advance-testing.png)                   |
| :----------------------------------------------------------: |
| **Figure 15. O branch do HEAD avança quando se faz um commit** |

```bash
$ git checkout master
```

|                ![](checkout-master.png)                |
| :----------------------------------------------------: |
| **Figura 16. O HEAD se move quando se faz o checkout** |

```bash
$ code test.rb
$ git commit -a -m 'made other changes'
```

|            ![](advance-master.png)             |
| :--------------------------------------------: |
| **Figura 17. Histórico de commits divergente** |

```bash
$ git log --oneline --graph
* c2b9e (HEAD, master) made other changes
| * 87ab2 (testing) made a change
|/
* f30ab add feature #32 - ability to add new formats to the
* 34ac2 fixed bug #1328 - stack overflow under certain conditions
* 98ca9 initial commit of my project
```

### 3.2 O Básico de Branch e Merge

1. Trabalhar um pouco em um website.
2. Criar um branch para uma nova estória de usuário na qual está trabalhando.
3. Trabalhar um pouco neste novo branch.
4. Mudar para seu branch de produção.
5. Criar um novo branch para fazer a correção.
6. Após testar, fazer o merge do branch de correção e fazer push para produção.
7. Voltar para sua estória de usuário original e continuar trabalhando.

#### Branching Básico

![Figura 18. Um histórico de commits simples](C:\Users\Semantix\Pro Git\basic-branching-1.png)

```bash
$ git checkout -b iss53
Switched to a new branch "iss53"
```

![Figura 19. Criando um novo branch](C:\Users\Semantix\Pro Git\basic-branching-2.png)

```bash
$ code index.html
$ git commit -a -m 'Create new footer [issue 53]'
```

![Figura 20. O branch `iss53` moveu para frente com seu trabalho](C:\Users\Semantix\Pro Git\basic-branching-3.png)

```bash
$ git checkout master
Switched to branch 'master'
```

```bash
$ git checkout -b hotfix
Switched to a new branch 'hotfix'
$ code index.html
$ git commit -a -m 'Fix broken email address'
[hotfix 1fb7853] Fix broken email address
 1 file changed, 2 insertions(+)
```

![Figura 21. Branch de hotfix baseado em `master`](C:\Users\Semantix\Pro Git\basic-branching-4.png)

```bash
$ git checkout master
$ git merge hotfix
Updating f42c576..3a0874c
Fast-forward
 index.html | 2 ++
 1 file changed, 2 insertions(+)
```

![Figura 22. O branch `master`  faz um fast-forward até `hotfix`](C:\Users\Semantix\Pro Git\basic-branching-5.png)

```bash
$ git branch -d hotfix
Deleted branch hotfix (3a0874c).
```

```bash
$ git checkout iss53
Switched to branch "iss53"
$ code index.html
$ git commit -a -m 'Finish the new footer [issue 53]'
[iss53 ad82d7a] Finish the new footer [issue 53]
1 file changed, 1 insertion(+)
```

![Figura 23. Continuando o trabalho no branch `iss53`](C:\Users\Semantix\Pro Git\basic-branching-6.png)

#### Merging Básico

```bash
$ git checkout master
Switched to branch 'master'
$ git merge iss53
Merge made by the 'recursive' strategy.
index.html |    1 +
1 file changed, 1 insertion(+)
```

![Figura 24. Três snapshots usados em um merge típico](C:\Users\Semantix\Pro Git\basic-merging-1.png)

![Figura 25. Um commit de merge](C:\Users\Semantix\Pro Git\basic-merging-2.png)

```bash
$ git branch -d iss53
```

#### Conflitos de Merge

```bash
$ git merge iss53
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

```bash
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)

    both modified:      index.html

no changes added to commit (use "git add" and/or "git commit -a")
```

```bash
<<<<<<< HEAD:index.html
<div id="footer">contact : email.support@github.com</div>
=======
<div id="footer">
 please contact us at support@github.com
</div>
>>>>>>> iss53:index.html
```

```bash
<div id="footer">
please contact us at email.support@github.com
</div>
```
```bash
$ git add index.html
$ git status
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:

    modified:   index.html
```
```bash
$ git commit
$ git branch -d iss53
$ git log --oneline --graph
*   3607e34 (HEAD -> master) Merge branch 'iss53' into master
|\
| * dae493c Mover footer para div em body
| * 13682d3 Criar novo footer [issue 53]
* | 56456a7 Consertar endereço de email quebrado
|/
* aabfc8c Iniciar html boilerplate
* 7b1cdb8 initial commit
```

### 3.3 Gerenciamento de Branches

```bash
$ git branch
  iss53
* master
  testing
```

```bash
$ git branch -v
  iss53   93b412c Fix javascript issue
* master  7a98805 Merge branch 'iss53'
  testing 782fd34 Add scott to the author list in the readme
```

```bash
$ git branch --merged
  iss53
* master
```

```bash
$ git branch --no-merged
  testing
```

```bash
$ git branch -d testing
error: The branch 'testing' is not fully merged.
If you are sure you want to delete it, run 'git branch -D testing'.
```

### 3.5 Remote Branches

![Figura 30. Repositório local e servidor após o clone](C:\Users\Semantix\Pro Git\remote-branches-1.png)

![Figura 31. Repositório local e remoto podem divergir](C:\Users\Semantix\Pro Git\remote-branches-2.png)

![Figura 32. `git fetch` atualiza suas preferências remotas](C:\Users\Semantix\Pro Git\remote-branches-3.png)

![Figura 33. Adicionando outro servidor como remoto](C:\Users\Semantix\Pro Git\remote-branches-4.png)

![Figura 34. Branch remoto de rastreamento para `teamone/master`](C:\Users\Semantix\Pro Git\remote-branches-5.png)

#### Fazendo o Push

```bash
$ git push origin serverfix
Counting objects: 24, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (15/15), done.
Writing objects: 100% (24/24), 1.91 KiB | 0 bytes/s, done.
Total 24 (delta 2), reused 0 (delta 0)
To https://github.com/schacon/simplegit
 * [new branch]      serverfix -> serverfix
```

```bash
$ git fetch origin
remote: Counting objects: 7, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0)
Unpacking objects: 100% (3/3), done.
From https://github.com/schacon/simplegit
 * [new branch]      serverfix    -> origin/serverfix
```

```bash
$ git checkout -b serverfix origin/serverfix
Branch serverfix set up to track remote branch serverfix from origin.
Switched to a new branch 'serverfix'
```

#### Tracking Branches

```bash
$ git checkout --track origin/serverfix
Branch serverfix set up to track remote branch serverfix from origin.
Switched to a new branch 'serverfix'
```
Isso é tão comum que existe até um atalho para isso. Se o nome do branch que você está tentando fazer o checkout (a) não existe e (b) corresponde exatamente a um nome em apenas um repositório remoto:
```bash
$ git checkout serverfix
Branch serverfix set up to track remote branch serverfix from origin.
Switched to a new branch 'serverfix'
```

```bash
$ git branch -u origin/serverfix
Branch serverfix set up to track remote branch serverfix from origin.
```

```bash
$ git fetch --all
$ git branch -vv
  iss53     7e424c3 [origin/iss53: ahead 2] forgot the brackets
  master    1ae2a45 [origin/master] deploying index fix
* serverfix f8674d9 [teamone/server-fix-good: ahead 3, behind 1] this should do it
  testing   5ea463a trying something new
```

#### Fazendo o Pull

Geralmente é melhor usar os comandos `fetch` e `merge` explicitamente, já que o `git pull` muitas vezes pode ser confuso

#### Removendo Branches Remotos

```bash
$ git push origin --delete serverfix
To https://github.com/schacon/simplegit
 - [deleted]         serverfix
```

### 3.6 Fazendo o Rebase

![Figure 35. Um simples histórico de divergência](C:\Users\Semantix\Pro Git\basic-rebase-1.png)

![Figura 36. Fazendo um merge para integrar áreas de trabalho que divergiram](C:\Users\Semantix\Pro Git\basic-merging-2.png)

```bash
$ git checkout experiment
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: added staged command
```

![Figura 37. Fazendo o rebase da mudança introduzida no `C4` em `C3`](C:\Users\Semantix\Pro Git\basic-rebase-3.png)

```bash
$ git checkout master
$ git merge experiment
```

#### Rebases Mais Interessantes

![Figure 39. Um histórico com um tópico de branch de outro branch](C:\Users\Semantix\Pro Git\interesting-rebase-1.png)

```bash
$ git rebase --onto master server client
```

![Figura 40. Fazendo rebase de um branch para outro branch](C:\Users\Semantix\Pro Git\interesting-rebase-2.png)

```bash
$ git checkout master
$ git merge client
```

![Figure 41. Fazendo fast-forward de seu branch `master` para incluir as mudanças da branch `client`](C:\Users\Semantix\Pro Git\interesting-rebase-3.png)

```bash
$ git rebase master server
```

![Figure 42. Fazendo rebase do branch `server` para o branch `master`](C:\Users\Semantix\Pro Git\interesting-rebase-4.png)

```bash
$ git checkout master
$ git merge server
```

```bash
$ git branch -d client
$ git branch -d server
```

![Figura 43. Histórico final de commits](C:\Users\Semantix\Pro Git\interesting-rebase-5.png)

#### Os Perigos do Rebase

**Não faça rebase de commits que existam fora de seu repositório e nos quais as pessoas possam ter trabalhado.**

![Figura 44. Fazendo clone de um repositório e trabalhando com ele](C:\Users\Semantix\Pro Git\perils-of-rebasing-1.png)

![Figura 45. Fazer fetch de mais commits e merge em seu trabalho](C:\Users\Semantix\Pro Git\perils-of-rebasing-2.png)

![Figura 46. Alguém faz um push de commits rebaseados abandonando commits nos quais você baseou seu trabalho](C:\Users\Semantix\Pro Git\perils-of-rebasing-3.png)

![Figura 47. Você faz o merge do mesmo trabalho novamente num novo commit de merge](C:\Users\Semantix\Pro Git\perils-of-rebasing-4.png)

#### Rebase sobre Rebase

![Figure 48. Rebase sobre trabalho de rebase forçado](C:\Users\Semantix\Pro Git\perils-of-rebasing-5.png)

#### Rebase vs. Merge

Dois pontos de vista sobre histórico:

* **Registro do que realmente aconteceu**
* **História de como o projeto foi feito**

### 3.7 Resumo

Cobrimos as funções de branching e merging básicas no Git. Você deve se sentir confortável para criar e alternar para novos branches, alternar entre branches e fazer merge de branches locais. Você também deve ser capaz de compartilhar seus branches fazendo push para um servidor compartilhado, trabalhando com outras pessoas em branches compartilhados e fazendo rebase de seus branches antes de serem compartilhados.

