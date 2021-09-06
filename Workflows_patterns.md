# Patterns para Gerenciar Branches de Código Fonte



## Patterns Base

### Branch Principal

Um único branch compartilhado que atua como o estado atual do produto.

### Branch Saldável

Em cada commit, executar verificações automatizadas, geralmente construindo e executando testes, para garantir que não haja defeitos no branch.

## Patterns de Integração

### Integração do Branch Principal

Os desenvolvedores integram seu trabalho fetchando do branch principal, mergeando e - se saudável - pushando de volta para o main branch.

### Branch de Feature

Coloque todo o trabalho para um feature em seu próprio branch, integre-o no branch principal quando o feature estiver concluído.

### Integração Contínua

Os desenvolvedores fazem a integração do branch principal assim que têm um commit saudável que podem compartilhar, geralmente menos que um dia de trabalho.

### Revisão Pré-integração

Cada commit para o branch principal é revisado por pares antes de o commit ser aceito.

## O Caminho entre Branch Branch e o Release para Produção

### Branch de Release

Um branch que aceita apenas commits aceitos para estabilizar uma versão do produto pronta para release.

### Branch de Maturidade

Um branch cujo head marca a versão mais recente de um nível de maturidade da base de código.

### Branch de Hotfix

Um branch para capturar trabalho para corrigir um defeito de produção urgente.

### Branch Principal Pronto para Release

Mantenha o branch principal suficientemente saldável para que o head do branch principal sempre possa ser colocado diretamente em produção.

## Outros Patterns de Branch

### Branch Experimental

Reúne trabalho experimental em uma base de código, que não se espera que seja mergeado diretamente no produto.

### Branch de Colaboração

Um branch criado para um desenvolvedor compartilhar trabalho com outros membros da equipe sem integração formal.

