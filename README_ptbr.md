# gnome-cedilla-fix

[English Version](README.md)

Este script configura o layout "US-International" do teclado no Linux para
gerar c cedilha (ç) ao invés de c acentuado (ć) quando a sequência `<acento> +
c` é digitada. O objetivo desse projeto é tornar o uso do teclado no padrão US-
International mais natural para usuários da língua portuguesa.

## Por que isso é necessário?

Desde as suas primeiras versões, o Microsoft Windows oferecia a opção de
teclado "US-International" onde letras acentuadas são geradas através da
sequência `<acento> + letra`. Este método se tornou bastante familiar para um
número grande de usuários, em particular para aqueles que começaram a usar
computadores antes da adoção do layout ABNT-II, ou que preferem o layout padrão
americano por outras razões.

Uma peculiaridade do teclado "US-International" no Windows é que a sequência
`<acento> + c` gera um c cedilha, ao invés de um c acentuado (que é menos comum
em linguagens latinas).  Esse comportamento foi traduzido literalmente para o X
e versões iniciais do Gnome.

Com o passar dos anos, a maioria dos países definiu seu próprio layout de
teclado (incluindo o Brasil, com o [infeliz] ABNT-II), e o projeto Gnome
adicionou suporte completo a esses layouts. Em determinado momento, os
desenvolvedores do Gnome decidiram que por questões de consistência, `[acento] + c` deveria gerar um c acentuado ao invés do cedilha.  A lógica é que a
maioria dos países já têm os seus teclados específicos e o "US-International"
seria uma espécie de "segunda opção" para aqueles usando o padrão americano.

Esta mudança gerou uma quantidade substancial de frustração, e
[vários](https://bugs.launchpad.net/ubuntu/+source/ibus/+bug/518056)
[bugs](http://askubuntu.com/questions/363115/how-to-type-latin-small-letter-c-with-cedilla)
[foram](https://ask.fedoraproject.org/en/question/28468/problems-with-letter-c-in-us-international-keyboard-fedora-19/)
[abertos](http://ubuntuforums.org/showthread.php?t=1851918)
[sobre o assunto](http://blog.klauskiwi.com/cedilla-c-symbol-using-american-keyboards-in-linux/)
sem uma solução clara. Este comportamento também causa confusão para usuários que migram de outros sistemas operacionais e torna a adoção do Linux mais complicada.

## Como usar

No prompt do shell, digite:

```bash
wget -q https://raw.githubusercontent.com/marcopaganini/gnome-cedilla-fix/master/fix-cedilla -O fix-cedilla
chmod 755 fix-cedilla
./fix-cedilla
```

Para ativar as modificações, faça um logout e outro login na sessão X. Se esse
procedimento não funcionar, reinicialize o seu computador.

## Desinstalação

A desinstalação é muito simples. Rode o comando abaixo:

```
rm "${HOME}/.XCompose"
```

Novamente, faça um logout/login para ativar as mudanças, ou reinicialize o seu computador.

## Funcionamento

O script faz uma cópia do arquivo "Compose" do OS para `~/.XCompose` (cópia
pessoal), traduzindo cada ocorrência de "c acentuado" (ć) para "c cedilha" (ç).
Este arquivo será usado pela sua sessão pessoal e determinará o comportamento
da sequência acento+c.

## Compatibilidade

Este programa foi testado com algumas versões do Debian, Ubuntu, Mint Linux e
Fedora com sucesso. Relatórios de sucesso ou problemas, _Pull Requests_ (PRs)
com consertos e atualizações são sempre bem-vindos.
