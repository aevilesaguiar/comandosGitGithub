#Comandos Git Github

##
--------------------------------
|||||||  VERSIONAMENTO |||||||||
--------------------------------

## GIT E GITHUB

- git init			// iniciar o git no diretório, uma linha do tempo
- git clone www.url.com	// clonar um repositório
- git pull			// puxa do repositório remoto. É igual a fazer git fetch + git merge
- git fetch			// igual ao git pull, mas não faz o merge(fusão) dos projetos
- git add nomArquivo	// add ou atualiza mudanças para irem para a linha do tempo
- git rm nomArquivo	// rm mudanças para irem para a linha do tempo
- git commit -m "msg"	// add um ponto na linha do tempo
- git status			// informa o estado das alterações do projeto
- git log				// mostra os pontos da linha do tempo, os commits --author="nome": busca por autor. --graph, mostra em forma gráfica o que tá acontecendo nas branches.
- git shortlog		// mostra contribuintes e numero de commits. -sn mostra apenas ranking por numero de commits
- git show			// apresenta determinado ponto na linha do tempo
- git branch			// cria nova branch, com o -D, deleta a branch
- git checkout		// muda de branch (anda pelas linha do tempo)
- git merge			// Unir linhas do tempo. Geralmente é mais usado quando se vai fazer pull requests.
- git push -u origin master	// primeiro comando pra subir arquivos pro servidor remoto quando não há.
- git push			// envia alterações locais para o repositório remoto
- git remote add origin www.url.com	// adiciona repositório remoto
- git diff			// Mostra alterações feitas em arquivos
- git stash			// salva temporariamente ambiente de desenvolvimento
- git stash list		// lista ambientes temporarios
- git stash apply		// aplica ambiente
- git stash drop		// exclui ambiente
- git bisect start	// 
- git bisect bad		// 
- git bisect good		// 
- git tag -a 1.0.0 -m "message"	// Cria tag de versão. para dar push é só add --tags ao comando push. git tag -d 1.0.0: Apaga tag local. Para apagar tag no repositório remoto, deve se usar git push origin :1.0.0
- git config --global alias.shortCutAAdd comandoGit	// Cria abreviatura de um comando.
- git merge		// Mescla branches criando novo commit agregador.
- git rebase		// Faz merge, mas sem criar novo commit, jogando commit da branch auxiliar pra frente da fila de commits. Usar com cuidado e fazer pull antes.
- git reflog		// 
- git reset		// dá unstage no arquivo.
-	--soft	// voltar o commitado pra staged.
-	--mixed	// voltar o commitado pra modified.
-	--hard	// mata tudo do commit e descarta todas as alterações.
	
  Para matar os commits, deve-se indicar a frente o commit que quer que se seja o final e não utilizar o commit que se quer que seja disfeito.
	É recomendado só utilizar se não tiver feito push pra repositório remoto, pq pode bagunçar a linha do tempo.
git clean		// 

## 
#####################################
##### CICLO DE TRABALHO COM GIT #####
#####################################

- git init

-  git add .
-  git status	// opcional para checar se foi add
-  git commit -m "mensagem aqui"

- git checkout -b nomeNewBranch	// cria branch nova e muda pra ela
- git checkout nomeArquivo.html	// Pega arquivo unstaged e retorna ao momento antes da alteração
- git reset HEAD arquivo.html		// Reseta arquivo staged para o commit mais recente: HEAD, ou seja, dá unstage.

- Para voltar a commits anteriores:
- git reset idDoCommit	// volta para commit antigo e vai a partir daí.
- git revert idDoCommit	// volta para commit antigo sem sobrescrever os subsequentes, ou seja, cria um commit novo que desfaz apenas o antigo acessado, sem apagar.

Guardar edição temporariamente para retomar desenvolvimento depois:
- git stash
[...]
- Faz edições no código, dá add, commit
[...]
- git stash list		// Mostra estados salvos para retomar desenvolvimento
- git stash pop		// Leva ao último estado salvo
- git stash apply stash@(0)	// Leva a stash específico, stash@(0) é o número do stash

Procurar commit quando não se sabe em qual se alterou algo:
- git bisect start
- git bisect bad HEAD		// Diz que commit atual tem alteração a desfazer
- git bisect good idDoCommit	// Indica que esse commit tá bom, ou seja, o commit de alteração que se procura está entre esses dois commits. O git vai dar um id de commit logo após isso e perguntar se esse é bom ou ruim.
- git bisect bad		// Caso commit sugerido seja ruim.
- git bisect good		// Caso commit sugerido seja bom.
- Entre bads e goods, o git encontra o arquivo exato da alteração.

Criar e trabalhar com branches:
- git checkout -b nomeNewBranch	// cria branch nova e muda pra ela
- git push -u origin nomeBrach	// -u diz que a branch da máquinda deve estar ligada a branch remota.
- git branch -r					// Mostra branches, com o -r mostra as branches remotas.
Ao fazer git pull, se obtem branches do repo remoto, mas localmente pode não haver branch correspondente. Usar git branch pra verificar.
- git branch -t design origin/design	// Cria branch local e associa a branch remota.

Resolvendo conflitos no git:
Quando o mesmo arquivo é alterado em diferentes lugares, o git sugere um merge. Quando são mudados pontos iguais, ele aponta o conflito.

## BOAS PRÁTICAS DE GIT:

1. Cada pessoa trabalhar na sua própria branch local.
	- git merge nomeBranchATrazer

Atualizar branch com base em outra:
	- git rebase branchBase branchAtualizar

Opções pra visualizar git log:
git log --pretty=oneline	// cod + nomeCommit em linha única
		--pretty=short		// mostra normalmente, mas sem datas
		--pretty=full		// todas infos no log

2. Rebase Git Workflow
	git checkout master				// Muda pra branch master
	git pull						// Atualiza branch master usando remota
	git checkout feature-branch		// Muda pra branch feature-branch
	git rebase master				// Rebase master
	git mergetool					// Encontrando algum conflito, tu resolve.
	git rebase --continue			// Após resolver, continua o rebase

	git rebase --abort		// Se fizer erro no merging, dá pra descartar alterações usando esse comando.
	git push -f				// Sobe as mudanças pro feature-branch repositório remoto.
	
3. Keeping your branches tidy
	git branch -m oldName newName	// Renomear outra branch que não a atual.
	git branch -m newName			// Renomear branch atual.
	git branch -d branchName		// Deleta branch
	
COMO FAZER CHERRY PICKING
git cherry-pick nDoCommit	// Trazer para a minha branch apenas um commit de outra branch

Fluxo de trabalho do github:
- Criar branch alternativa baseada na master
- Trabalhar nessa branch (adds e commits)
- Fazer git pull na master 
- Fazer merge da alternativa na master
- Fazer push da master pro remoto

Fluxo Open Source:
- Faz fork do repositório de interesse.
- Clona o fork para o ambiente local.
- Configura remote origin para apontar para o nosso fork do oficial.
- Configura remote upstream para apontar para o repositório oficial.
	- Isso possibilita ter atualizações baseadas no repositório oficial. Nesse caso se usa o git pull upstream para puxar do upstream.
- Seguir com o desenvolvimento no estilo github flow ou outro que quiser.

COMMITS SEMÂNTICOS:
fix - Commits do tipo fix indicam que seu trecho de código commitado está solucionando um problema (bug fix), (se relaciona com o PATCH do versionamento semântico).

feat - Commits do tipo feat indicam que seu trecho de código está incuindo um novo recurso (se relaciona com o MINOR do versionamento semântico).
docs - Commits do tipo docs indicam que houveram mudanças na documentação, como por exemplo no Readme do seu repositório. (Não inclui alterações em código).

style - Commits do tipo style indicam que houveram alterações referentes a formatações de código, semicolons, trailing spaces, lint... (Não inclui alterações em código).

refactor - Commits do tipo refactor referem-se a mudanças devido a refatorações que não alterem sua funcionalidade, como por exemplo, uma alteração no formato como é processada determinada parte da tela, mas que manteve a mesma funcionalidade, ou melhorias de performance devido a um code review.

build - Commits do tipo build são utilizados quando são realizadas modificações em arquivos de build e dependências.

test - Commits do tipo test são utilizados quando são realizadas alterações em testes, seja criando, alterando ou excluindo testes unitários. (Não inclui alterações em código)

chore - Commits do tipo chore indicam atualizações de tarefas de build, configurações de administrador, pacotes... como por exemplo adicionar um pacote no gitignore. (Não inclui alterações em código)

BREAKING CHANGE - Commits que possuem o texto BREAKING CHANGE no começo do corpo opcional ou no rodapé opcional, indicam que a modificação que está sendo realizada no commit, possui uma modificiação que quebra a compatibilidade da API, (se relaciona com o MAJOR do versionamento semântico).

------------------
|| WORKFLOW GITFLOW ||
------------------

ORGANIZAÇÃO DAS BRANCHES

 Master
    |______Develop
    |           |______Feature
    |           |       |
    |  Release  | MERGE |
    |     |     |_______/
    |     |-----|
    |_____/     |
    |           |
    |\          |
    | `--Hotfix |
    |__-´       |
    |           |


GIT FILE STATUS LIFECYCLE:

UNTRACKED | UNMODIFIED | MODIFIED | STAGED
add file --->
			edit file -----> 
						stage file ---->
<--------- remove file
				<------------------- commit
____________________________________________
