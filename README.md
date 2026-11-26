# ontem

Retoma as sessões do [Claude Code](https://claude.com/claude-code) do dia anterior sem precisar abrir o terminal em cada pasta.

Lista a última sessão de cada pasta (de todas as contas, inclusive perfis do [CCS](https://github.com/kaitranntt/ccs)) e abre as escolhidas, cada uma numa aba do Windows Terminal, já na pasta certa e com `-r <id>`.

```
$ ontem
 1  qui 00:30  ~/Projetos/projeto-a  [claude]
      Ajuste no fluxo de login
 2  qua 19:21  ~/Projetos/projeto-b  [ccs personal]
      Problema das Lambdas na AWS

Abrir quais? (ex.: 1 3 4, t = todas, Enter = nenhuma):
```

## Uso

| Comando | O que faz |
|---|---|
| `ontem` | Sessões das últimas 24h (na segunda, desde sexta) |
| `ontem 3` | Sessões dos últimos 3 dias |
| `ontem -a` | Todas as sessões, não só a última por pasta |

O título é o nome dado com `/rename` ou, se não houver, o título automático do Claude Code. Sessões de script (`claude -p`, entrypoint `sdk-cli`), pastas em `/tmp` e pastas que não existem mais ficam de fora.

## Onde procura as sessões

- `~/.claude/projects`: reaberta com `claude`
- `~/.ccs/instances/<perfil>/projects`: reaberta com `ccs <perfil>`

## Requisitos

- WSL2 com Windows Terminal (`wt.exe`) e Python 3
- Ajuste `WT_PROFILE` no script para o GUID do seu perfil WSL, que fica no `settings.json` do Windows Terminal

## Instalação

```bash
git clone https://github.com/EduardoMeira/ontem.git
ln -s "$PWD/ontem/ontem" ~/.local/bin/ontem
```

## Detalhe do Windows Terminal

O `wt.exe` trata `;` como separador dos próprios comandos, então o comando da aba usa `|| true && exec bash` no lugar de `; exec bash`. Sem isso, cada sessão abriria uma aba extra com erro.
