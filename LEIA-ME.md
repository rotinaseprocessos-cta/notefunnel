# NoteFunnel

Ferramenta estilo Miro (quadro em branco, nós arrastáveis, post-its, conexões,
marcadores, mapa mental) pra desenhar o funil de qualquer cliente. Antes se
chamava "Mapa do Funil" — o nome mudou, o arquivo e os dados continuam os
mesmos.

Desde a última evolução, **é um arquivo único pra todos os clientes** — não
precisa mais copiar o `index.html` e trocar nome por cliente. Cada cliente
vira um "projeto" dentro do próprio arquivo (menu **Projetos**), guardado na
mesma tabela Supabase que já sincronizava o estado antes.

## Como funciona

- **Estado por projeto** salva sozinho no `localStorage` da máquina e também
  sincroniza com o Supabase (tabela `funil_mapas`) — assim dá pra abrir o
  mesmo cliente de qualquer navegador/computador, não só o que editou por
  último.
- **Botão "Projetos"** (ícone de pasta no menu lateral) abre a lista de
  clientes já salvos (nome + data da última edição) e permite:
  - **Abrir** um projeto existente.
  - **Criar** um projeto novo — só digitar o nome do cliente.
- Na primeira vez que abrir o arquivo (sem nenhum projeto salvo ainda nesse
  navegador), ele pergunta o nome do cliente antes de mostrar o quadro.
- Botão **"Novo quadro em branco"** limpa o projeto atual (nós, conexões,
  post-its, marcadores, imagens) e recomeça do zero — útil se quiser
  reaproveitar o mesmo projeto do zero sem apagar os outros clientes.
- **"Salvar projeto"** exporta um `.json` de backup do projeto atual;
  **"Abrir projeto"** importa um `.json` salvo por este mapa.
- **"Exportar imagem"** baixa um PNG do quadro inteiro (usa a biblioteca
  `html2canvas` carregada via internet — é a única função do arquivo que
  precisa de conexão; todo o resto funciona offline, inclusive local
  `file:///...`).

## Mapa mental

Duas formas, pra dois usos diferentes:

- **Árvore de cards**: com um card normal (`.node`) selecionado, **Tab** cria
  um card-filho à direita já conectado, **Enter** cria um card-irmão embaixo
  conectado ao mesmo pai. Bom pra estruturar etapas do funil em árvore.
- **Mapa mental (estilo brainstorm, igual Whimsical)**: botão dedicado no
  menu lateral cria um nó central em formato de pill ("Ideia central"). Pra
  criar um ramo, **passe o mouse sobre o nó e arraste o pontinho azul que
  aparece na borda até um espaço vazio** — cria e já conecta um ramo novo
  (texto colorido, sem caixa, linha curva) no lugar onde soltar. Também dá
  pra arrastar até outro nó existente pra conectar os dois. Cada galho que
  sai direto do centro ganha uma cor nova (roda entre verde-água/magenta/
  azul/dourado/laranja); os filhos de um galho herdam a cor dele. Quem
  preferir teclado: com um nó selecionado, Tab/Enter também funcionam.
- **Colapsar/expandir**: todo nó que tem ramos ganha uma bolinha na borda
  (aparece perto da linha de conexão). Clicar nela recolhe todos os
  descendentes daquele ramo e mostra só um número (quantos itens estão
  escondidos ali); clicar de novo expande.

## Selecionar vários e excluir em massa

- **Arrastar no vazio do quadro** agora abre uma caixa de seleção (igual
  Whimsical/Miro) — solta em cima de tudo que quiser selecionar. Com a
  seleção feita, `Delete`/`Backspace` exclui todos de uma vez, sem pedir
  confirmação.
- `Ctrl+A` seleciona tudo que está visível no quadro inteiro, do mesmo jeito.
- Como arrastar no vazio virou seleção, pra **navegar pelo quadro** (pan) use
  a rodinha/gesto de duas dedos do touchpad (já funciona direto), ou segure
  **Espaço** e arraste.

## Imagens

- Colar da área de transferência (Ctrl+V) já funciona como antes.
- Agora também dá pra inserir direto do PC pelo botão de imagem no menu
  lateral (aceita várias de uma vez).

## Modo claro/escuro

Botão de sol/lua no menu lateral alterna o tema. A preferência fica salva no
navegador (`localStorage`), separada de cada projeto.

## Como publicar

Publicar o arquivo `index.html` uma vez só, num único domínio — como agora é
multi-cliente, não precisa de um deploy por cliente. O deploy em si (domínio
próprio, GitHub, etc.) fica por conta de quem estiver publicando.

## Conexões em ângulo reto (cotovelo)

Ao selecionar uma seta (entre cards) ou um ramo do mapa mental, além de
Contínua/Tracejada agora tem **Cotovelo** — o traço vira um caminho em
ângulo reto (com cantos arredondados) em vez da curva suave padrão.

## Texto solto (ferramenta "Novo texto")

Corrigido: o texto agora acompanha o tema (claro/escuro) por padrão, em vez
de ficar sempre escuro (o que o deixava quase invisível no modo escuro).
Selecionando um texto solto também aparece uma paleta de cores — inclusive
uma opção "automática" pra voltar a seguir o tema.

## Se quiser ir além no futuro

Existe um app completo de whiteboard (fork do `mcp-excalidraw`, com Kanban,
mapa mental nativo, banco de logos, servidor Node/Express+SQLite+WebSocket)
que pode virar a base de uma versão própria mais robusta mais pra frente —
fica registrado como próximo passo, não faz parte deste arquivo.
