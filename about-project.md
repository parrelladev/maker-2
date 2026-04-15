# Maker - About the Project

## 1. Visao geral

O Maker e uma ferramenta interna de redacao para transformar links de noticias em layouts pre-definidos para publicacao no Instagram. O sistema deve rodar localmente, preferencialmente como uma aplicacao Electron, coletar informacoes de uma noticia, aplicar esses dados em templates visuais feitos em HTML/CSS e gerar imagens prontas para uso em redes sociais.

## 2. Objetivo do produto

Permitir que jornalistas que trabalham na distribuicao de noticias para redes sociais informem a URL de uma noticia, selecionem um layout pre-definido, editem os campos quando necessario, visualizem uma previa da arte gerada e baixem a imagem final para publicacao no Instagram.

## 3. Publico-alvo

Jornalistas que trabalham na distribuicao de noticias para redes sociais dentro de uma redacao jornalistica. O uso previsto e interno, restrito a equipe da redacao.

## 4. Problema que o sistema resolve

O processo manual de criacao de artes para redes sociais a partir de noticias pode ser demorado, repetitivo e sujeito a inconsistencias visuais. O Maker busca automatizar parte desse processo, coletando os dados da noticia, aplicando esses dados em layouts pre-definidos e gerando imagens prontas para publicacao no Instagram.

## 5. Escopo inicial

O sistema deve contemplar:

- Coleta de metadados de links de sites de noticia.
- Uso de templates em HTML e CSS preenchidos automaticamente com os metadados coletados.
- Geracao de imagem PNG a partir do template usando a biblioteca `html-to-image`.
- Selecao de template na tela inicial.
- Uso inicial de 5 templates ja prontos em HTML e CSS.
- Interface para editar manualmente os campos da arte quando necessario.
- Preview da arte antes da criacao final.
- Download da imagem gerada.
- Selecao de imagem local quando a imagem da noticia nao for suficiente ou nao for coletada.
- Selecao de cor/tema para templates que tenham variacoes visuais.
- Geracao de post para feed do Instagram no formato 1080x1440.
- Geracao de story para Instagram.
- Geracao simultanea de mais de um formato quando o usuario selecionar multiplos layouts.

## 6. Fora de escopo

- Publicacao automatica em redes sociais.
- Edicao avancada de imagem no estilo Photoshop/Figma.
- Criacao de artes sem vinculacao com uma URL de noticia, salvo se isso for definido como necessidade futura.
- Historico completo de artes geradas, salvo se for definido como requisito da primeira versao.
- Builder visual de templates na primeira versao.
- Login e autenticacao na primeira versao.

## 7. Atores do sistema

### Ator principal - Usuario criador de arte

Jornalista responsavel por transformar uma noticia em uma arte para redes sociais. Esse usuario acessa o sistema, escolhe um template, informa a URL, revisa o preview e baixa o PNG.

### Ator secundario - Administrador de templates

Pessoa responsavel por criar, configurar ou manter os templates disponiveis no sistema. Esse ator pode ser o proprio desenvolvedor ou uma pessoa da equipe com permissao para configurar modelos.

### Sistema externo - Site de noticia

Fonte de onde serao coletados os metadados da noticia, como titulo, imagem, editoria, autor e data.

## 8. Casos de uso

### UC01 - Gerar arte para Instagram a partir de uma noticia

Ator principal: usuario criador de arte.

Fluxo principal:

1. O usuario acessa a tela inicial.
2. O usuario escolhe diretamente um ou mais cards de layout, como "Feed - Template 1" ou "Story - Template 2".
3. Cada card selecionado representa um formato e um template especifico.
4. O usuario informa a URL de uma noticia.
5. O sistema inicia automaticamente a coleta dos metadados da noticia.
6. O sistema exibe um indicador de carregamento durante a coleta.
7. O sistema monta o preview com template, textos, imagem, background, tema e logo.
8. O sistema preenche os layouts selecionados com os mesmos dados iniciais coletados da noticia.
9. O usuario edita manualmente os campos quando necessario.
10. O sistema permite ajustes independentes de texto e imagem em cada layout selecionado.
11. O usuario seleciona um layout no grid de previews para coloca-lo em foco.
12. O sistema exibe no painel de edicao os campos do layout selecionado.
13. O sistema atualiza o preview com as alteracoes.
14. O usuario pode duplicar um layout para testar variacoes de texto, tema ou imagem.
15. O usuario clica em criar.
16. O sistema valida se todos os campos obrigatorios foram preenchidos.
17. O sistema gera a arte em PNG.
18. O sistema aplica a nomenclatura definida para o arquivo.
19. O sistema baixa a imagem gerada.

Fluxos alternativos:

- Se a URL for invalida, o sistema deve informar que nao conseguiu reconhecer a noticia.
- Se os metadados nao forem encontrados, o sistema deve informar quais campos estao ausentes.
- Se a coleta automatica falhar, o sistema deve exibir a mensagem: "Nao foi possivel coletar os dados. Preencha os campos manualmente."
- Se a coleta automatica falhar, o campo de URL deve ser limpo para que o usuario possa colar outra URL.
- Se a URL tiver espacos ou texto extra, o sistema deve apontar erro, sem tentar corrigir automaticamente.
- Se a imagem principal nao puder ser carregada, o sistema deve permitir substituir ou preencher manualmente a imagem antes da geracao.
- Se o texto ultrapassar o limite visual do template, o sistema nao deve cortar ou ajustar automaticamente; o usuario deve identificar o problema no preview e editar manualmente.
- Se algum campo obrigatorio estiver pendente, o sistema nao deve permitir gerar a imagem ate que o usuario preencha o campo manualmente.
- Se o usuario deixar a URL vazia, o sistema deve permitir gerar a imagem desde que todos os campos obrigatorios sejam preenchidos manualmente.

### UC02 - Configurar template

Ator principal: administrador de templates.

Fluxo principal:

1. O administrador acessa a area ou estrutura de configuracao de templates.
2. O administrador define nome, dimensao, campos, layout e variacoes de cor do template.
3. O sistema salva ou disponibiliza o template para uso.
4. O template passa a aparecer na lista de opcoes para o usuario criador de arte.

Observacao: o builder visual de templates fica previsto como funcionalidade futura. Na primeira versao, os templates serao criados diretamente em HTML e CSS.

## 9. Requisitos funcionais

### RF01 - Selecionar template

O sistema deve permitir que o usuario escolha um ou mais layouts a partir de cards na tela inicial. Cada card deve representar uma combinacao de formato e template.

### RF02 - Escolher formato de publicacao

O sistema deve permitir que o usuario escolha layouts para os formatos de feed e story para Instagram.

### RF03 - Pesquisar e filtrar layouts

O sistema deve permitir pesquisar e filtrar os cards de layout por formato e tema.

### RF04 - Informar URL da noticia

O sistema deve permitir que o usuario informe a URL de uma noticia publicada em um site jornalistico.

### RF05 - Coletar metadados da noticia

O sistema deve coletar os metadados necessarios da noticia informada, como titulo, subtitulo, imagem principal, editoria, autor, data e outros campos que forem definidos como necessarios.

### RF06 - Coletar metadados automaticamente

O sistema deve iniciar a coleta dos metadados automaticamente quando o usuario informar ou colar uma URL.

### RF07 - Preencher tag automaticamente

O sistema deve preencher o campo `tag` automaticamente com a editoria ou categoria da noticia quando essa informacao estiver disponivel.

### RF08 - Exibir carregamento da coleta

O sistema deve exibir um indicador de carregamento enquanto busca os metadados da noticia.

### RF09 - Tratar falha na coleta

O sistema deve exibir a mensagem "Nao foi possivel coletar os dados. Preencha os campos manualmente." quando nao conseguir coletar os metadados da URL.

### RF10 - Limpar URL apos erro de coleta

Quando a coleta automatica falhar, o sistema deve limpar o campo de URL para que o usuario possa colar outra URL.

### RF11 - Permitir preenchimento manual sem URL

O sistema deve permitir gerar a imagem sem URL quando o usuario deixar o campo de URL vazio, desde que todos os campos obrigatorios sejam preenchidos manualmente.

### RF12 - Preencher template automaticamente

O sistema deve preencher o template selecionado com os metadados coletados da noticia.

### RF13 - Editar campos manualmente

O sistema deve permitir que o usuario edite manualmente os campos da arte antes da geracao, incluindo tag, titulo, subtitulo e imagem.

### RF14 - Editar campos por layout

O sistema deve permitir que o usuario ajuste texto e imagem separadamente em cada layout selecionado.

### RF15 - Selecionar imagem local

O sistema deve permitir que o usuario selecione uma imagem local pelo explorador de arquivos para substituir ou preencher a imagem da noticia.

### RF16 - Encaixar imagem no template

O sistema deve encaixar a imagem selecionada no template, sem oferecer ferramenta de recorte manual na primeira versao.

### RF17 - Exibir preview da arte

O sistema deve exibir uma previa da arte antes da geracao final.

### RF18 - Atualizar preview apos edicao

O sistema deve atualizar o preview da arte quando o usuario alterar manualmente algum campo.

### RF19 - Exibir previews em grid

O sistema deve exibir os layouts selecionados em um grid de previews para permitir comparacao visual rapida.

### RF20 - Destacar layout selecionado

O sistema deve permitir selecionar um layout no grid, aplicando estado de foco ou destaque visual para indicar qual layout esta sendo editado.

### RF21 - Editar layout em painel unico

O sistema deve exibir os campos editaveis em um painel unico, atualizado dinamicamente conforme o layout selecionado no grid.

### RF22 - Duplicar layout selecionado

O sistema deve permitir duplicar um layout selecionado para testar variacoes de texto, tema ou imagem. A duplicacao deve criar uma nova instancia independente no grid de previews.

### RF23 - Nomear copia de layout automaticamente

O sistema deve atribuir um nome automatico para layouts duplicados, como `Template 1 - copia` ou `Template 1 - variacao 2`.

### RF24 - Remover instancia duplicada

O sistema deve permitir que o usuario remova do grid uma instancia duplicada que nao deseja mais usar.

### RF25 - Permitir selecao de cor/tema

O sistema deve permitir que o usuario selecione uma variacao de cor quando o template possuir mais de uma opcao visual.

### RF26 - Validar campos obrigatorios

O sistema deve verificar se os campos obrigatorios foram preenchidos antes de permitir a geracao da imagem.

### RF27 - Gerar imagem PNG

O sistema deve gerar uma imagem PNG a partir do layout HTML/CSS usando a biblioteca `html-to-image`.

### RF28 - Gerar multiplos formatos simultaneamente

O sistema deve permitir que o usuario selecione mais de um formato/layout e gere as imagens selecionadas em uma unica acao, desde que todos os previews selecionados estejam validos.

### RF29 - Desmarcar layout antes da geracao

O sistema deve permitir que o usuario remova da geracao um formato/layout que nao ficou adequado no preview, mantendo os demais selecionados.

### RF30 - Baixar imagem gerada

O sistema deve permitir que o usuario baixe a imagem gerada.

### RF31 - Baixar arquivos separados

Quando mais de uma imagem for gerada, o sistema deve baixar arquivos separados, um para cada formato/layout selecionado.

### RF32 - Aplicar nomenclatura padrao ao arquivo

O sistema deve nomear automaticamente a imagem gerada seguindo o padrao `{formato}-{titulo-em-slug}-{data}.png`.

### RF33 - Exibir mensagem de sucesso

O sistema deve exibir a mensagem "Imagem baixada com sucesso" apos o download das imagens.

### RF34 - Abrir pasta de downloads

O sistema deve permitir que o usuario abra a pasta de downloads apos gerar as imagens.

### RF35 - Usar templates em HTML e CSS

O sistema deve permitir o uso de templates criados em HTML e CSS, para que diferentes layouts possam ser adicionados ao projeto.

### RF36 - Aplicar tema visual do template

O sistema deve permitir que o usuario escolha uma variacao visual pre-definida do template, aplicando o arquivo CSS correspondente ao tema selecionado.

### RF37 - Builder de template

O sistema deve oferecer uma forma de criar, configurar ou editar templates em uma fase futura do projeto.

## 10. Requisitos nao funcionais

### RNF01 - Execucao local ou simplificada

O sistema deve funcionar localmente, preferencialmente como uma aplicacao Electron, sem depender de infraestrutura complexa para a primeira versao.

### RNF02 - Desempenho na coleta de dados

O sistema deve coletar os metadados da noticia em tempo adequado para uso operacional. Meta inicial: retornar os dados em ate 3 segundos em uma conexao estavel, quando a pagina de origem estiver disponivel.

### RNF03 - Desempenho na geracao da imagem

O sistema deve gerar o PNG em tempo adequado para uso operacional. Meta inicial: gerar a imagem em ate 5 segundos apos o clique em criar, considerando um template ja carregado.

### RNF04 - Usabilidade

A interface deve ser simples o suficiente para que um usuario consiga gerar uma imagem seguindo o fluxo principal sem precisar alterar codigo ou manipular arquivos manualmente.

### RNF05 - Acessibilidade

O sistema deve considerar boas praticas de acessibilidade, incluindo contraste adequado, navegacao por teclado e textos compreensiveis para leitores de tela nos controles principais.

### RNF06 - Qualidade visual da imagem

O PNG gerado deve preservar a fidelidade visual do template selecionado, mantendo proporcao, fontes, cores, imagens e posicionamento dos elementos conforme o preview.

### RNF07 - Manutenibilidade dos templates

Os templates devem ser organizados de forma que novas artes possam ser adicionadas ou ajustadas com baixo esforco, sem exigir alteracoes profundas no funcionamento principal do sistema.

### RNF08 - Compatibilidade

O sistema deve funcionar como aplicacao Electron em Windows, macOS e Linux. Caso exista uma versao web no futuro, os navegadores suportados devem ser definidos posteriormente.

### RNF09 - Confiabilidade da exportacao

O sistema deve evitar gerar arquivos corrompidos ou vazios. Caso a exportacao falhe, deve exibir uma mensagem de erro clara para o usuario.

### RNF10 - Seguranca e autenticacao

Na primeira versao, o sistema nao precisa exigir login, pois o uso previsto e local e interno. A possibilidade de autenticacao via Microsoft pode ser avaliada em uma fase futura caso o sistema passe a ter distribuicao centralizada, dados sensiveis, historico de uso ou acesso por rede.

## 11. Regras de negocio

### RN01 - Origem das noticias

O sistema deve aceitar links de sites de noticia. A coleta dependera da disponibilidade de metadados na pagina informada.

### RN02 - Geracao somente apos preview

O usuario deve conseguir revisar a arte em preview antes de baixar a imagem final.

### RN03 - Variacao visual por template

Um mesmo template pode ter variacoes de cor/tema, e o usuario deve poder escolher entre as variacoes disponiveis.

### RN04 - Formatos iniciais de publicacao

Na primeira versao, o sistema deve gerar imagens para Instagram nos formatos feed 1080x1440 e story 1080x1920.

### RN05 - Uso interno

O sistema sera utilizado somente por profissionais da redacao.

### RN06 - Campos obrigatorios

Para gerar a imagem, os campos tag, titulo, subtitulo e imagem devem estar preenchidos. Quando o sistema nao conseguir coletar algum desses campos, o usuario deve preencher manualmente antes de gerar a arte.

### RN07 - Templates baseados em HTML

Qualquer template podera ser usado pelo Maker desde que seja implementado em HTML e CSS e siga a estrutura esperada pelo sistema.

### RN08 - Nomenclatura do arquivo

As imagens geradas devem seguir o padrao `{formato}-{titulo-em-slug}-{data}.png`.

{formato} - `feed` ou `story`, em minusculo
{titulo-em-slug} - Titulo da noticia convertido para slug, com limite maximo de 80 caracteres
{data} - Data em que a imagem foi gerada, no formato `DD-MM-YYYY`

### RN09 - Sem limite automatico de caracteres

O sistema nao deve impor limite automatico de caracteres para tag, titulo e subtitulo na primeira versao. O usuario deve verificar no preview se o texto ficou adequado ao layout.

### RN10 - Geracao de formatos selecionados

O sistema deve gerar simultaneamente apenas os formatos/layouts selecionados pelo usuario.

### RN11 - Download separado por imagem

Quando o usuario gerar mais de uma imagem na mesma acao, cada imagem deve ser salva como um arquivo separado, sem compactacao em `.zip` na primeira versao.

### RN12 - Pasta padrao de downloads

Os arquivos gerados devem ser salvos na pasta padrao de downloads do sistema operacional.

### RN13 - Edicao independente por layout

Como cada layout pode responder de forma diferente ao mesmo conteudo, o sistema deve permitir ajustes independentes por formato/layout selecionado. Os layouts podem iniciar com os mesmos dados coletados, mas a alteracao feita em um preview nao precisa ser aplicada automaticamente aos demais.

### RN14 - Temas pre-definidos por template

As variacoes de cor/tema devem ser pre-definidas pelo proprio template. Cada template pode ter uma quantidade diferente de temas, e o sistema deve permitir que novas variacoes sejam adicionadas com simplicidade.

### RN15 - Selecao por card de layout

O usuario deve escolher diretamente cards de layout, em vez de escolher primeiro o formato e depois o template. Cada card deve indicar claramente qual template e qual formato serao gerados.

### RN16 - Campo tag

O campo usado para representar o chapeu/editoria da noticia deve ser chamado internamente de `tag`.

### RN17 - Logo fixa por template

A logo deve ser fixa em cada template. Templates diferentes podem possuir logos diferentes, mas o usuario nao precisa trocar a logo manualmente na primeira versao.

### RN18 - Cards sem miniatura obrigatoria

Os cards de layout nao precisam exibir miniatura previa na primeira versao.

### RN19 - Tag automatica por editoria

Quando o site de noticia informar editoria ou categoria, o sistema deve usar essa informacao para preencher automaticamente o campo `tag`.

### RN20 - Tag pendente

Quando o sistema nao conseguir identificar a editoria ou categoria da noticia, o campo `tag` deve ficar vazio para preenchimento manual.

### RN21 - Filtros de layout

Na primeira versao, os filtros de layout devem considerar formato e tema.

### RN22 - Card sem miniatura real

Quando o card de layout nao tiver uma miniatura especifica do template, ele deve exibir uma imagem generica com a logo do veiculo definida pelo proprio template.

### RN23 - Preview em grid

Os layouts selecionados devem ser exibidos em grid para facilitar comparacao visual entre opcoes.

### RN24 - Painel unico de edicao

Os campos editaveis devem ficar em um painel unico, preferencialmente a esquerda, e devem mudar conforme o layout selecionado no grid. O painel pode ser recolhivel.

### RN25 - Duplicacao independente

Ao duplicar um layout, o sistema deve criar uma nova instancia independente, permitindo testar variacoes de texto, tema ou imagem sem alterar o layout original.

### RN26 - Informacoes do card de layout

Cada card de layout deve exibir somente nome e formato, alem da imagem generica com a logo do veiculo quando nao houver miniatura especifica.

### RN27 - Sem sincronizacao global de edicao

O sistema nao precisa oferecer uma acao para aplicar o mesmo texto ou imagem em todos os layouts depois que eles ja foram editados separadamente.

### RN28 - Coleta automatica por URL

A coleta dos metadados deve ser iniciada automaticamente quando o usuario informar ou colar a URL da noticia.

### RN29 - Sem validacao previa de tipo de URL

O sistema nao precisa validar previamente se a URL parece ser uma noticia. Ele deve tentar coletar os metadados e informar campos pendentes quando nao conseguir obter os dados necessarios.

### RN30 - Sem persistencia de configuracoes locais

Na primeira versao, o sistema nao precisa salvar configuracoes locais, como ultimo tema usado, layouts recentes ou preferencias do usuario.

### RN31 - Mensagem de falha na coleta

Quando a coleta automatica falhar, o sistema deve exibir a mensagem: "Nao foi possivel coletar os dados. Preencha os campos manualmente."

### RN32 - URL invalida sem correcao automatica

Quando a URL informada tiver espacos ou texto extra, o sistema deve apontar erro e nao deve tentar limpar ou corrigir automaticamente o texto informado.

### RN33 - Geracao sem URL

O sistema deve permitir gerar imagens sem URL quando o campo de URL estiver vazio, desde que os campos obrigatorios sejam preenchidos manualmente.

### RN34 - Formulario manual minimo

O formulario manual deve conter apenas os campos obrigatorios da primeira versao: tag, titulo, subtitulo e imagem.

### RN35 - Sem botao de limpar tudo

O sistema nao precisa oferecer um botao especifico para limpar todos os campos e recomecar na primeira versao.

### RN36 - Selecao de imagem local

A imagem local deve ser selecionada pelo explorador de arquivos. O sistema nao precisa aceitar arrastar e soltar imagem na primeira versao.

### RN37 - Sem recorte manual de imagem

O sistema deve apenas encaixar a imagem no template. Nao precisa oferecer ferramenta de corte ou recorte manual na primeira versao.

### RN38 - Exportacao somente em PNG

Na primeira versao, o sistema deve exportar sempre em PNG.

### RN39 - Resolucao exata de saida

As imagens geradas devem respeitar exatamente as dimensoes definidas para cada formato: feed 1080x1440 e story 1080x1920.

### RN40 - Sem bloqueio por baixa resolucao da imagem

O sistema nao deve impedir a geracao caso a imagem local tenha baixa resolucao. O usuario deve avaliar o resultado pelo preview.

### RN41 - Mensagem de sucesso apos download

Depois de baixar as imagens, o sistema deve exibir a mensagem "Imagem baixada com sucesso".

### RN42 - Slug no nome do arquivo

O titulo usado no nome do arquivo deve ser convertido para slug, removendo acentos, caracteres especiais e espacos.

### RN43 - Limite do slug

O slug do titulo no nome do arquivo deve ter no maximo 80 caracteres para evitar nomes de arquivo muito longos.

### RN44 - Formato da data no arquivo

A data usada no nome do arquivo deve seguir o formato `DD-MM-YYYY`, por exemplo `15-04-2026`.

### RN45 - Formato em minusculo no arquivo

O formato usado no nome do arquivo deve ser `feed` ou `story`, sempre em minusculo.

### RN46 - Abrir pasta de downloads

Apos gerar as imagens, o sistema deve permitir abrir a pasta padrao de downloads.

## 12. Dados e metadados

Campos inicialmente previstos:

- URL da noticia.
- Site de origem da noticia.
- Tag.
- Titulo.
- Subtitulo.
- Imagem.
- Editoria/categoria.
- Autor.
- Data de publicacao.
- Logo.
- Tema/cor selecionado.
- Caminho ou arquivo local da imagem selecionada manualmente.

Campos a confirmar:

- Tags.
- Credito da imagem.
- Texto alternativo da imagem.
- Data de atualizacao.
- Nome do template.

## 13. Templates

O projeto deve aceitar templates criados em HTML e CSS. A estrutura interna dos templates ainda nao precisa ser fechada, mas cada template deve fornecer ao sistema as informacoes necessarias para ser preenchido e exportado corretamente.

Informacoes que cada template deve conseguir informar ao sistema:

- Nome do template.
- Formato de saida, como feed ou story.
- Dimensoes da imagem exportada.
- Campos que o template utiliza.
- Campos obrigatorios.
- Variacoes de tema/cor disponiveis.
- Forma de aplicar os dados da noticia no layout.
- Logo fixa do template.
- Fontes e assets necessarios, quando houver.

Informacoes definidas:

- Quantidade inicial de templates: 5 templates prontos em HTML e CSS.
- Dimensoes de saida: feed 1080x1440 e story 1080x1920.
- Campos obrigatorios por template: tag, titulo, subtitulo e imagem.
- Sem limite automatico de caracteres para tag, titulo e subtitulo.
- As variacoes de cor/tema devem ser pre-definidas pelo template.
- Cada template deve definir como os campos do sistema serao aplicados no HTML, sem obrigar uma estrutura tecnica especifica nesta etapa do projeto.

Informacoes a definir:

- Campos opcionais por template.
- Lista final de temas disponiveis para cada um dos 5 templates.
- Uso de marcas, fontes e assets institucionais.

## 14. Nomenclatura dos arquivos

Padrao definido:

```text
{formato}-{titulo-em-slug}-{data}.png
```

## 15. Restricoes e dependencias

- O sistema deve usar `html-to-image` para transformar os templates em PNG.
- O sistema deve rodar localmente, preferencialmente com Electron.
- A coleta de metadados depende da estrutura e dos metadados disponiveis nas paginas dos sites de noticia.
- A execucao local pode exigir tratamento para restricoes de CORS, proxy local ou coleta via backend.

## 16. Riscos e pontos de atencao

- Mudancas no HTML ou nos metadados dos sites de noticia podem quebrar a coleta automatica.
- Imagens externas podem ter bloqueios de CORS ao serem renderizadas no canvas.
- Textos longos podem quebrar o layout dos templates.
- Diferencas entre navegadores podem afetar a fidelidade da imagem gerada.
- Fontes externas podem nao carregar corretamente antes da exportacao.

## 17. Criterios de aceite iniciais

- O usuario consegue selecionar layouts por cards na tela inicial.
- O usuario consegue pesquisar e filtrar cards de layout.
- O usuario consegue filtrar layouts por formato e tema.
- O usuario consegue escolher entre feed 1080x1440 e story 1080x1920.
- O usuario consegue informar uma URL valida de uma noticia.
- O sistema inicia automaticamente a coleta apos a URL ser informada.
- O sistema exibe indicador de carregamento durante a coleta.
- O sistema consegue coletar os principais metadados da noticia.
- O sistema exibe a mensagem definida quando a coleta falha.
- O sistema limpa o campo de URL apos erro de coleta.
- O sistema consegue montar um preview com os dados coletados.
- O usuario consegue preencher todos os campos manualmente e gerar imagem sem URL.
- O usuario consegue editar manualmente tag, titulo, subtitulo e imagem.
- O usuario consegue fazer ajustes independentes por layout selecionado.
- O sistema exibe os previews em grid.
- O sistema destaca o layout selecionado para edicao.
- O painel unico de edicao atualiza conforme o layout selecionado.
- O painel de edicao pode ser recolhido.
- O usuario consegue duplicar um layout e editar a copia de forma independente.
- O layout duplicado recebe nome automatico.
- O usuario consegue remover uma instancia duplicada do grid.
- O usuario consegue selecionar uma imagem local.
- A imagem local e selecionada pelo explorador de arquivos.
- A imagem selecionada e encaixada no template sem recorte manual.
- O preview e atualizado apos edicoes manuais.
- O sistema bloqueia a geracao quando algum campo obrigatorio esta vazio.
- O sistema permite gerar mais de um formato/layout selecionado ao mesmo tempo.
- O sistema permite desmarcar um layout que nao ficou adequado no preview.
- O usuario consegue gerar e baixar um arquivo PNG.
- Quando mais de uma imagem e gerada, o sistema baixa arquivos separados.
- Os arquivos sao salvos na pasta padrao de downloads.
- O arquivo baixado segue a nomenclatura `{formato}-{titulo-em-slug}-{data}.png`.
- A data do arquivo segue o formato `DD-MM-YYYY`.
- O formato do arquivo usa `feed` ou `story` em minusculo.
- O slug do titulo tem no maximo 80 caracteres.
- O arquivo gerado sempre esta em PNG.
- O arquivo gerado respeita exatamente a resolucao do formato selecionado.
- O sistema nao bloqueia a geracao por baixa resolucao da imagem local.
- O sistema exibe a mensagem "Imagem baixada com sucesso" apos baixar as imagens.
- O usuario consegue abrir a pasta de downloads apos gerar as imagens.
- O sistema informa erro quando a URL e invalida ou quando os dados nao podem ser coletados.

## 18. Referencias do professor

Orientacoes recebidas:

- Requisitos nao funcionais nao descrevem necessariamente uma funcionalidade do sistema.
- Requisitos nao funcionais podem tratar de desempenho, acessibilidade, seguranca, usabilidade, compatibilidade e qualidade.
- O documento deve descrever as funcionalidades, identificar quem vai usar, como vai usar e quais sao os atores envolvidos.

Imagens/modelo classico: a anexar ou descrever.

## 19. Perguntas em aberto

1. Quais navegadores precisam ser oficialmente suportados caso exista versao web alem do Electron?
2. A primeira versao precisa ter tela de configuracao ou tudo pode vir definido nos arquivos do projeto?
3. O aplicativo deve ter modo claro/escuro proprio ou seguir apenas a interface definida?
4. O sistema deve exibir erros de validacao campo a campo ou apenas uma mensagem geral?
5. O sistema precisa ter algum tutorial, ajuda ou texto explicativo dentro da interface?
