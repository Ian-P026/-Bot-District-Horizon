# District Horizon — Bot de Whitelist

Bot Discord em Node.js 20+ / discord.js 14.

## Instalação

1. Extraia o ZIP e mantenha seu `.env` local (não publique o token no GitHub).
2. Execute `npm install`.
3. Configure os IDs no `.env` conforme `.env.example`.
4. Convide o bot com os escopos `bot` e `applications.commands`.
5. Permissões recomendadas: Ver canais, Enviar mensagens, Incorporar links, Ler histórico, Usar comandos de aplicação e Gerenciar cargos. Ative `Server Members Intent` no Developer Portal. Para o atalho `//vagas`, habilite também `Message Content Intent`.
6. Execute `npm start`.

## Comandos

- `//vagas` — publica no canal atual o painel de formulários (requer Gerenciar servidor e Message Content Intent).
- `/vagas` — alternativa por comando de aplicação.
- `/whitelist` — atalho para abrir o formulário padrão PLAYERS.
- `/formulario-criar nome descricao perguntas` — cria um formulário. Separe as perguntas usando `|` (de 1 a 20).
- `/formulario-editar nome-atual novo-nome descricao perguntas` — edita um formulário personalizado. O novo nome é opcional; informe novamente a lista completa de perguntas, separadas por `|`.
- `/formulario-remover nome` — remove um formulário personalizado.
- `/formulario-listar` — lista os formulários disponíveis.

Os comandos de administração exigem a permissão Gerenciar servidor. Depois de criar, editar ou remover formulários, execute `/vagas` novamente para publicar um painel atualizado.

## Formulário padrão PLAYERS

O formulário padrão é mantido no próprio bot e pode ser iniciado pelo botão PLAYERS no painel `/vagas` ou pelo comando `/whitelist`.

Formulários com mais de cinco perguntas são divididos em etapas, respeitando o limite de componentes de modal do Discord.

## Canais e cargos

Edite os IDs no `.env`. O cargo de aprovado precisa estar abaixo do cargo do bot na hierarquia. O bot não lê mensagens de outros bots, não monitora canal externo e não depende do Koya/Coia. As inscrições são iniciadas pelos botões do painel próprio publicado com `/vagas` ou `//vagas`.

## Persistência

Formulários e decisões ficam no SQLite em `./data/whitelist.sqlite`. Não apague a pasta `data` ao atualizar o bot. Inscrições em andamento (antes do envio) ficam em memória e precisam ser reiniciadas se o processo for reiniciado.

Opcional: defina `SUPPORT_CHANNEL_ID` no `.env` para que o painel mencione diretamente o canal de suporte.

## Motivos prontos para reprovação

Administradores com a permissão **Gerenciar servidor** podem cadastrar motivos que aparecerão como opções ao clicar em **Reprovar** no painel de análise:

- `/motivo-criar texto:<motivo>` — adiciona um motivo pronto.
- `/motivo-listar` — mostra os motivos cadastrados.
- `/motivo-remover motivo:<motivo>` — remove um motivo (selecione pela sugestão/autocomplete).

Também é possível escolher **Escrever outro motivo** para informar um texto personalizado. Em resultados de reprovação, as respostas do candidato não são publicadas; somente a decisão, a identificação/foto do candidato, o avaliador e o motivo são exibidos.

## Gerenciar formulários

`/formulario-listar`, `/formulario-editar` e `/formulario-remover` agora oferecem sugestões de nomes (autocomplete). Ao editar, informe apenas os campos que deseja alterar. O formulário PLAYERS padrão pode ser editado e suas alterações também serão usadas pelo comando `/whitelist`; ele continua protegido contra remoção.

O painel `//vagas` usa o nome do servidor como título e menciona os canais configurados em `RESULT_CHANNEL_ID` e `SUPPORT_CHANNEL_ID`.
