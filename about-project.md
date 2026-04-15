# Maker - Sobre o Projeto

## 1. Visão Geral

O Maker é uma ferramenta interna de redação para transformar links de notícias em layouts pré-definidos para publicação no Instagram. O sistema deve rodar localmente, preferencialmente como uma aplicação Electron, coletar informações de uma notícia, aplicar esses dados em templates visuais feitos em HTML/CSS e gerar imagens prontas para uso em redes sociais.

## 2. Objetivo do Produto

Permitir que jornalistas responsáveis pela distribuição de notícias em redes sociais informem a URL de uma notícia, selecionem um layout pré-definido, editem os campos quando necessário, visualizem uma prévia da arte gerada e baixem a imagem final para publicação no Instagram.

## 3. Público-Alvo

Jornalistas que trabalham na distribuição de notícias para redes sociais dentro de uma redação jornalística. O uso previsto é interno, restrito à equipe da redação.

## 4. Problema que o Sistema Resolve

O processo manual de criação de artes para redes sociais a partir de notícias pode ser demorado, repetitivo e sujeito a inconsistências visuais. O Maker busca automatizar parte desse processo, coletando os dados da notícia, aplicando esses dados em layouts pré-definidos e gerando imagens prontas para publicação no Instagram.

## 5. Escopo Inicial

O sistema deve contemplar:

- Coleta de metadados de links de sites de notícia.
- Uso de templates em HTML e CSS preenchidos automaticamente com os metadados coletados.
- Geração de imagem PNG a partir do template usando a biblioteca `html-to-image`.
- Abertura direta na lista de layouts.
- Seleção de layout por cards.
- Uso inicial de 5 templates prontos em HTML e CSS.
- Interface para edição manual dos campos da arte quando necessário.
- Preview da arte antes da geração final.
- Download da imagem gerada.
- Seleção de imagem local quando a imagem da notícia não for suficiente ou não for coletada.
- Seleção de tema/cor para templates que tenham variações visuais.
- Modo claro e modo escuro na interface do aplicativo.
- Geração de post para feed do Instagram no formato 1080x1440.
- Geração de story para Instagram no formato 1080x1920.
- Geração simultânea de mais de um formato quando o usuário selecionar múltiplos layouts.
- Validação campo a campo dos dados obrigatórios.

## 6. Fora de Escopo

- Publicação automática em redes sociais.
- Edição avançada de imagem no estilo Photoshop/Figma.
- Criação de artes sem dados manuais ou sem campos obrigatórios preenchidos.
- Histórico completo de artes geradas.
- Builder visual de templates na primeira versão.
- Login e autenticação na primeira versão.
- Tela de configuração na primeira versão.
- Área de ajuda, tutorial ou documentação dentro da interface na primeira versão.
- Botão para limpar todos os campos e recomeçar.
- Recorte manual de imagem.
- Arrastar e soltar imagem local.
- Exportação em formatos diferentes de PNG.

## 7. Atores do Sistema

### Ator principal - Usuário criador de arte

Jornalista responsável por transformar uma notícia em uma arte para redes sociais. Esse usuário acessa o sistema, escolhe um layout, informa a URL ou preenche os campos manualmente, revisa o preview e baixa o PNG.

### Ator secundário - Administrador de templates

Pessoa responsável por criar, configurar ou manter os templates disponíveis no sistema. Esse ator pode ser o próprio desenvolvedor ou uma pessoa da equipe com permissão para configurar modelos.

### Sistema externo - Site de notícia

Fonte de onde serão coletados os metadados da notícia, como título, imagem, editoria, autor e data.

## 8. Casos de Uso

### UC01 - Gerar arte para Instagram a partir de uma notícia

Ator principal: usuário criador de arte.

Fluxo principal:

1. O usuário abre o aplicativo.
2. O sistema exibe diretamente a lista de layouts.
3. O usuário escolhe um ou mais cards de layout, como `Feed - Template 1` ou `Story - Template 2`.
4. Cada card selecionado representa um formato e um template específico.
5. O usuário informa a URL de uma notícia.
6. O sistema inicia automaticamente a coleta dos metadados da notícia.
7. O sistema exibe um indicador de carregamento durante a coleta.
8. O sistema preenche os layouts selecionados com os dados coletados da notícia.
9. O sistema monta o preview com template, textos, imagem, tema e logo.
10. O usuário edita manualmente os campos quando necessário.
11. O sistema permite ajustes independentes de texto e imagem em cada layout selecionado.
12. O usuário seleciona um layout no grid de previews para colocá-lo em foco.
13. O sistema exibe no painel de edição os campos do layout selecionado.
14. O sistema atualiza o preview com as alterações.
15. O usuário pode duplicar um layout para testar variações de texto, tema ou imagem.
16. O usuário clica em criar.
17. O sistema valida campo a campo se todos os campos obrigatórios foram preenchidos.
18. O sistema gera a arte em PNG.
19. O sistema aplica a nomenclatura definida para o arquivo.
20. O sistema baixa a imagem gerada na pasta padrão de downloads.
21. O sistema exibe a mensagem `Imagem baixada com sucesso`.
22. O usuário pode abrir a pasta de downloads.

Fluxos alternativos:

- Se a URL for inválida, o sistema deve apontar erro.
- Se os metadados não forem encontrados, o sistema deve informar os campos pendentes.
- Se a coleta automática falhar, o sistema deve exibir a mensagem: `Não foi possível coletar os dados. Preencha os campos manualmente.`
- Se a coleta automática falhar, o campo de URL deve ser limpo para que o usuário possa colar outra URL.
- Se a URL tiver espaços ou texto extra, o sistema deve apontar erro, sem tentar corrigir automaticamente.
- Se a imagem principal não puder ser carregada, o sistema deve permitir substituir ou preencher manualmente a imagem antes da geração.
- Se o texto ultrapassar o limite visual do template, o sistema não deve cortar ou ajustar automaticamente; o usuário deve identificar o problema no preview e editar manualmente.
- Se algum campo obrigatório estiver pendente, o sistema não deve permitir gerar a imagem até que o usuário preencha o campo.
- Se o usuário deixar a URL vazia, o sistema deve permitir gerar a imagem desde que todos os campos obrigatórios sejam preenchidos manualmente.

### UC02 - Configurar template

Ator principal: administrador de templates.

Fluxo principal:

1. O administrador edita os arquivos do projeto responsáveis pelos templates.
2. O administrador define nome, dimensão, campos, layout, logo e variações de tema do template.
3. O sistema passa a disponibilizar o template na lista de layouts.

Observação: o builder visual de templates fica previsto como funcionalidade futura. Na primeira versão, os templates serão criados e configurados diretamente nos arquivos do projeto.

## 9. Requisitos Funcionais

### RF01 - Abrir diretamente na lista de layouts

O sistema deve abrir diretamente na lista de layouts, sem uma tela inicial anterior.

### RF02 - Selecionar layout

O sistema deve permitir que o usuário escolha um ou mais layouts a partir de cards. Cada card deve representar uma combinação de formato e template.

### RF03 - Escolher formato de publicação

O sistema deve permitir que o usuário escolha layouts para os formatos de feed e story do Instagram.

### RF04 - Pesquisar e filtrar layouts

O sistema deve permitir pesquisar e filtrar os cards de layout por formato e tema.

### RF05 - Informar URL da notícia

O sistema deve permitir que o usuário informe a URL de uma notícia publicada em um site jornalístico.

### RF06 - Coletar metadados da notícia

O sistema deve coletar os metadados necessários da notícia informada, como título, subtítulo, imagem principal, editoria, autor, data e outros campos que forem definidos como necessários.

### RF07 - Coletar metadados automaticamente

O sistema deve iniciar a coleta dos metadados automaticamente quando o usuário informar ou colar uma URL.

### RF08 - Preencher tag automaticamente

O sistema deve preencher o campo `tag` automaticamente com a editoria ou categoria da notícia quando essa informação estiver disponível.

### RF09 - Exibir carregamento da coleta

O sistema deve exibir um indicador de carregamento enquanto busca os metadados da notícia.

### RF10 - Tratar falha na coleta

O sistema deve exibir a mensagem `Não foi possível coletar os dados. Preencha os campos manualmente.` quando não conseguir coletar os metadados da URL.

### RF11 - Limpar URL após erro de coleta

Quando a coleta automática falhar, o sistema deve limpar o campo de URL para que o usuário possa colar outra URL.

### RF12 - Permitir preenchimento manual sem URL

O sistema deve permitir gerar a imagem sem URL quando o usuário deixar o campo de URL vazio, desde que todos os campos obrigatórios sejam preenchidos manualmente.

### RF13 - Preencher template automaticamente

O sistema deve preencher o template selecionado com os metadados coletados da notícia.

### RF14 - Editar campos manualmente

O sistema deve permitir que o usuário edite manualmente os campos da arte antes da geração, incluindo `tag`, título, subtítulo e imagem.

### RF15 - Editar campos por layout

O sistema deve permitir que o usuário ajuste texto e imagem separadamente em cada layout selecionado.

### RF16 - Selecionar imagem local

O sistema deve permitir que o usuário selecione uma imagem local pelo explorador de arquivos para substituir ou preencher a imagem da notícia.

### RF17 - Encaixar imagem no template

O sistema deve encaixar a imagem selecionada no template, sem oferecer ferramenta de recorte manual na primeira versão.

### RF18 - Exibir preview da arte

O sistema deve exibir uma prévia da arte antes da geração final.

### RF19 - Atualizar preview após edição

O sistema deve atualizar o preview da arte quando o usuário alterar manualmente algum campo.

### RF20 - Exibir previews em grid

O sistema deve exibir os layouts selecionados em um grid de previews para permitir comparação visual rápida.

### RF21 - Destacar layout selecionado

O sistema deve permitir selecionar um layout no grid, aplicando estado de foco ou destaque visual para indicar qual layout está sendo editado.

### RF22 - Editar layout em painel único

O sistema deve exibir os campos editáveis em um painel único, atualizado dinamicamente conforme o layout selecionado no grid.

### RF23 - Recolher painel de edição

O sistema deve permitir que o painel de edição seja recolhido.

### RF24 - Duplicar layout selecionado

O sistema deve permitir duplicar um layout selecionado para testar variações de texto, tema ou imagem. A duplicação deve criar uma nova instância independente no grid de previews.

### RF25 - Nomear cópia de layout automaticamente

O sistema deve atribuir um nome automático para layouts duplicados, como `Template 1 - cópia` ou `Template 1 - variação 2`.

### RF26 - Remover instância duplicada

O sistema deve permitir que o usuário remova do grid uma instância duplicada que não deseja mais usar.

### RF27 - Permitir seleção de tema

O sistema deve permitir que o usuário selecione uma variação de tema quando o template possuir mais de uma opção visual.

### RF28 - Validar campos obrigatórios

O sistema deve verificar campo a campo se os campos obrigatórios foram preenchidos antes de permitir a geração da imagem.

### RF29 - Exibir erros campo a campo

O sistema deve exibir erros de validação diretamente nos campos que precisam de correção.

### RF30 - Gerar imagem PNG

O sistema deve gerar uma imagem PNG a partir do layout HTML/CSS usando a biblioteca `html-to-image`.

### RF31 - Gerar múltiplos formatos simultaneamente

O sistema deve permitir que o usuário selecione mais de um formato/layout e gere as imagens selecionadas em uma única ação, desde que todos os previews selecionados estejam válidos.

### RF32 - Desmarcar layout antes da geração

O sistema deve permitir que o usuário remova da geração um formato/layout que não ficou adequado no preview, mantendo os demais selecionados.

### RF33 - Baixar imagem gerada

O sistema deve permitir que o usuário baixe a imagem gerada.

### RF34 - Baixar arquivos separados

Quando mais de uma imagem for gerada, o sistema deve baixar arquivos separados, um para cada formato/layout selecionado.

### RF35 - Aplicar nomenclatura padrão ao arquivo

O sistema deve nomear automaticamente a imagem gerada seguindo o padrão `{formato}-{titulo-em-slug}-{data}.png`.

### RF36 - Exibir mensagem de sucesso

O sistema deve exibir a mensagem `Imagem baixada com sucesso` após o download das imagens.

### RF37 - Abrir pasta de downloads

O sistema deve permitir que o usuário abra a pasta de downloads após gerar as imagens.

### RF38 - Usar templates em HTML e CSS

O sistema deve permitir o uso de templates criados em HTML e CSS, para que diferentes layouts possam ser adicionados ao projeto.

### RF39 - Aplicar tema visual do template

O sistema deve permitir que o usuário escolha uma variação visual pré-definida do template, aplicando o tema correspondente.

### RF40 - Alternar modo claro e escuro

O sistema deve permitir alternar a interface do aplicativo entre modo claro e modo escuro.

### RF41 - Configurar templates por arquivos do projeto

O sistema deve permitir que templates e variações sejam definidos nos arquivos do projeto, sem exigir uma tela de configuração na primeira versão.

### RF42 - Builder de template

O sistema deve oferecer uma forma de criar, configurar ou editar templates em uma fase futura do projeto.

## 10. Requisitos Não Funcionais

### RNF01 - Execução local

O sistema deve funcionar localmente, preferencialmente como uma aplicação Electron, sem depender de infraestrutura complexa para a primeira versão.

### RNF02 - Desempenho na coleta de dados

O sistema deve coletar os metadados da notícia em tempo adequado para uso operacional. Meta inicial: retornar os dados em até 3 segundos em uma conexão estável, quando a página de origem estiver disponível.

### RNF03 - Desempenho na geração da imagem

O sistema deve gerar o PNG em tempo adequado para uso operacional. Meta inicial: gerar a imagem em até 5 segundos após o clique em criar, considerando um template já carregado.

### RNF04 - Usabilidade

A interface deve ser simples o suficiente para que um usuário consiga gerar uma imagem seguindo o fluxo principal sem precisar alterar código ou manipular arquivos manualmente.

### RNF05 - Acessibilidade

O sistema deve considerar boas práticas de acessibilidade, incluindo contraste adequado, navegação por teclado e textos compreensíveis para leitores de tela nos controles principais.

### RNF06 - Qualidade visual da imagem

O PNG gerado deve preservar a fidelidade visual do template selecionado, mantendo proporção, fontes, cores, imagens e posicionamento dos elementos conforme o preview.

### RNF07 - Manutenibilidade dos templates

Os templates devem ser organizados de forma que novas artes possam ser adicionadas ou ajustadas com baixo esforço, sem exigir alterações profundas no funcionamento principal do sistema.

### RNF08 - Compatibilidade

O sistema deve funcionar como aplicação Electron em Windows, macOS e Linux. Caso exista uma versão web no futuro, os navegadores suportados devem ser definidos posteriormente.

### RNF09 - Confiabilidade da exportação

O sistema deve evitar gerar arquivos corrompidos ou vazios. Caso a exportação falhe, deve exibir uma mensagem de erro clara para o usuário.

### RNF10 - Segurança e autenticação

Na primeira versão, o sistema não precisa exigir login, pois o uso previsto é local e interno. A possibilidade de autenticação via Microsoft pode ser avaliada em uma fase futura caso o sistema passe a ter distribuição centralizada, dados sensíveis, histórico de uso ou acesso por rede.

## 11. Regras de Negócio

### RN01 - Origem das notícias

O sistema deve aceitar links de sites de notícia. A coleta dependerá da disponibilidade de metadados na página informada.

### RN02 - Geração somente após preview

O usuário deve conseguir revisar a arte em preview antes de baixar a imagem final.

### RN03 - Variação visual por template

Um mesmo template pode ter variações de tema, e o usuário deve poder escolher entre as variações disponíveis.

### RN04 - Formatos iniciais de publicação

Na primeira versão, o sistema deve gerar imagens para Instagram nos formatos feed 1080x1440 e story 1080x1920.

### RN05 - Uso interno

O sistema será utilizado somente por profissionais da redação.

### RN06 - Campos obrigatórios

Para gerar a imagem, os campos `tag`, título, subtítulo e imagem devem estar preenchidos. Quando o sistema não conseguir coletar algum desses campos, o usuário deve preencher manualmente antes de gerar a arte.

### RN07 - Templates baseados em HTML

Qualquer template poderá ser usado pelo Maker desde que seja implementado em HTML e CSS e siga a estrutura esperada pelo sistema.

### RN08 - Nomenclatura do arquivo

As imagens geradas devem seguir o padrão `{formato}-{titulo-em-slug}-{data}.png`.

- `{formato}`: `feed` ou `story`, em minúsculo.
- `{titulo-em-slug}`: título da notícia convertido para slug, com limite máximo de 80 caracteres.
- `{data}`: data em que a imagem foi gerada, no formato `DD-MM-YYYY`.

### RN09 - Sem limite automático de caracteres no conteúdo

O sistema não deve impor limite automático de caracteres para `tag`, título e subtítulo na primeira versão. O usuário deve verificar no preview se o texto ficou adequado ao layout.

### RN10 - Geração de formatos selecionados

O sistema deve gerar simultaneamente apenas os formatos/layouts selecionados pelo usuário.

### RN11 - Download separado por imagem

Quando o usuário gerar mais de uma imagem na mesma ação, cada imagem deve ser salva como um arquivo separado, sem compactação em `.zip` na primeira versão.

### RN12 - Pasta padrão de downloads

Os arquivos gerados devem ser salvos na pasta padrão de downloads do sistema operacional.

### RN13 - Edição independente por layout

Como cada layout pode responder de forma diferente ao mesmo conteúdo, o sistema deve permitir ajustes independentes por formato/layout selecionado. Os layouts podem iniciar com os mesmos dados coletados, mas a alteração feita em um preview não precisa ser aplicada automaticamente aos demais.

### RN14 - Temas pré-definidos por template

As variações de tema devem ser pré-definidas pelo próprio template. Cada template pode ter uma quantidade diferente de temas, e o sistema deve permitir que novas variações sejam adicionadas com simplicidade.

### RN15 - Seleção por card de layout

O usuário deve escolher diretamente cards de layout, em vez de escolher primeiro o formato e depois o template. Cada card deve indicar claramente qual template e qual formato serão gerados.

### RN16 - Campo tag

O campo usado para representar o chapéu/editoria da notícia deve ser chamado internamente de `tag`.

### RN17 - Logo fixa por template

A logo deve ser fixa em cada template. Templates diferentes podem possuir logos diferentes, mas o usuário não precisa trocar a logo manualmente na primeira versão.

### RN18 - Cards sem miniatura obrigatória

Os cards de layout não precisam exibir miniatura prévia na primeira versão.

### RN19 - Tag automática por editoria

Quando o site de notícia informar editoria ou categoria, o sistema deve usar essa informação para preencher automaticamente o campo `tag`.

### RN20 - Tag pendente

Quando o sistema não conseguir identificar a editoria ou categoria da notícia, o campo `tag` deve ficar vazio para preenchimento manual.

### RN21 - Filtros de layout

Na primeira versão, os filtros de layout devem considerar formato e tema.

### RN22 - Card sem miniatura real

Quando o card de layout não tiver uma miniatura específica do template, ele deve exibir uma imagem genérica com a logo do veículo definida pelo próprio template.

### RN23 - Preview em grid

Os layouts selecionados devem ser exibidos em grid para facilitar a comparação visual entre opções.

### RN24 - Painel único de edição

Os campos editáveis devem ficar em um painel único, preferencialmente à esquerda, e devem mudar conforme o layout selecionado no grid. O painel pode ser recolhível.

### RN25 - Duplicação independente

Ao duplicar um layout, o sistema deve criar uma nova instância independente, permitindo testar variações de texto, tema ou imagem sem alterar o layout original.

### RN26 - Informações do card de layout

Cada card de layout deve exibir somente nome e formato, além da imagem genérica com a logo do veículo quando não houver miniatura específica.

### RN27 - Sem sincronização global de edição

O sistema não precisa oferecer uma ação para aplicar o mesmo texto ou imagem em todos os layouts depois que eles já foram editados separadamente.

### RN28 - Coleta automática por URL

A coleta dos metadados deve ser iniciada automaticamente quando o usuário informar ou colar a URL da notícia.

### RN29 - Sem validação prévia de tipo de URL

O sistema não precisa validar previamente se a URL parece ser uma notícia. Ele deve tentar coletar os metadados e informar campos pendentes quando não conseguir obter os dados necessários.

### RN30 - Sem persistência de configurações locais

Na primeira versão, o sistema não precisa salvar configurações locais, como último tema usado, layouts recentes ou preferências do usuário.

### RN31 - Mensagem de falha na coleta

Quando a coleta automática falhar, o sistema deve exibir a mensagem: `Não foi possível coletar os dados. Preencha os campos manualmente.`

### RN32 - URL inválida sem correção automática

Quando a URL informada tiver espaços ou texto extra, o sistema deve apontar erro e não deve tentar limpar ou corrigir automaticamente o texto informado.

### RN33 - Geração sem URL

O sistema deve permitir gerar imagens sem URL quando o campo de URL estiver vazio, desde que os campos obrigatórios sejam preenchidos manualmente.

### RN34 - Formulário manual mínimo

O formulário manual deve conter apenas os campos obrigatórios da primeira versão: `tag`, título, subtítulo e imagem.

### RN35 - Sem botão de limpar tudo

O sistema não precisa oferecer um botão específico para limpar todos os campos e recomeçar na primeira versão.

### RN36 - Seleção de imagem local

A imagem local deve ser selecionada pelo explorador de arquivos. O sistema não precisa aceitar arrastar e soltar imagem na primeira versão.

### RN37 - Sem recorte manual de imagem

O sistema deve apenas encaixar a imagem no template. Não precisa oferecer ferramenta de corte ou recorte manual na primeira versão.

### RN38 - Exportação somente em PNG

Na primeira versão, o sistema deve exportar sempre em PNG.

### RN39 - Resolução exata de saída

As imagens geradas devem respeitar exatamente as dimensões definidas para cada formato: feed 1080x1440 e story 1080x1920.

### RN40 - Sem bloqueio por baixa resolução da imagem

O sistema não deve impedir a geração caso a imagem local tenha baixa resolução. O usuário deve avaliar o resultado pelo preview.

### RN41 - Mensagem de sucesso após download

Depois de baixar as imagens, o sistema deve exibir a mensagem `Imagem baixada com sucesso`.

### RN42 - Slug no nome do arquivo

O título usado no nome do arquivo deve ser convertido para slug, removendo acentos, caracteres especiais e espaços.

### RN43 - Limite do slug

O slug do título no nome do arquivo deve ter no máximo 80 caracteres para evitar nomes de arquivo muito longos.

### RN44 - Formato da data no arquivo

A data usada no nome do arquivo deve seguir o formato `DD-MM-YYYY`, por exemplo `15-04-2026`.

### RN45 - Formato em minúsculo no arquivo

O formato usado no nome do arquivo deve ser `feed` ou `story`, sempre em minúsculo.

### RN46 - Abrir pasta de downloads

Após gerar as imagens, o sistema deve permitir abrir a pasta padrão de downloads.

### RN47 - Configurações via arquivos do projeto

Na primeira versão, as configurações de templates, temas e assets devem vir dos arquivos do projeto, sem uma tela de configuração no aplicativo.

### RN48 - Modo claro e escuro

O aplicativo deve oferecer modo claro e modo escuro para a interface.

### RN49 - Validação campo a campo

Os erros de validação devem aparecer nos campos específicos que precisam de correção.

### RN50 - Sem tutorial interno

Na primeira versão, o sistema não precisa ter área de tutorial, ajuda ou textos explicativos extensos dentro da interface.

### RN51 - Entrada direta na lista de layouts

Ao abrir o aplicativo, o usuário deve ser levado diretamente para a lista de layouts.

## 12. Dados e Metadados

Campos inicialmente previstos:

- URL da notícia.
- Site de origem da notícia.
- Tag.
- Título.
- Subtítulo.
- Imagem.
- Editoria/categoria.
- Autor.
- Data de publicação.
- Logo.
- Tema selecionado.
- Caminho ou arquivo local da imagem selecionada manualmente.

Campos a confirmar:

- Crédito da imagem.
- Texto alternativo da imagem.
- Data de atualização.
- Nome do template.

## 13. Templates

O projeto deve aceitar templates criados em HTML e CSS. A estrutura interna dos templates ainda não precisa ser fechada, mas cada template deve fornecer ao sistema as informações necessárias para ser preenchido e exportado corretamente.

Informações que cada template deve conseguir informar ao sistema:

- Nome do template.
- Formato de saída, como feed ou story.
- Dimensões da imagem exportada.
- Campos que o template utiliza.
- Campos obrigatórios.
- Variações de tema disponíveis.
- Forma de aplicar os dados da notícia no layout.
- Logo fixa do template.
- Fontes e assets necessários, quando houver.

Informações definidas:

- Quantidade inicial de templates: 5 templates prontos em HTML e CSS.
- Dimensões de saída: feed 1080x1440 e story 1080x1920.
- Campos obrigatórios por template: `tag`, título, subtítulo e imagem.
- Sem limite automático de caracteres para `tag`, título e subtítulo.
- As variações de tema devem ser pré-definidas pelo template.
- Cada template deve definir como os campos do sistema serão aplicados no HTML, sem obrigar uma estrutura técnica específica nesta etapa do projeto.
- As configurações dos templates devem vir dos arquivos do projeto.

Informações a definir:

- Campos opcionais por template.
- Lista final de temas disponíveis para cada um dos 5 templates.
- Uso de marcas, fontes e assets institucionais.

## 14. Nomenclatura dos Arquivos

Padrão definido:

```text
{formato}-{titulo-em-slug}-{data}.png
```

Exemplo:

```text
feed-minha-noticia-importante-15-04-2026.png
```

## 15. Restrições e Dependências

- O sistema deve usar `html-to-image` para transformar os templates em PNG.
- O sistema deve rodar localmente, preferencialmente com Electron.
- A coleta de metadados depende da estrutura e dos metadados disponíveis nas páginas dos sites de notícia.
- A execução local pode exigir tratamento para restrições de CORS, proxy local ou coleta via backend.
- A primeira versão deve funcionar em Windows, macOS e Linux.

## 16. Riscos e Pontos de Atenção

- Mudanças no HTML ou nos metadados dos sites de notícia podem quebrar a coleta automática.
- Imagens externas podem ter bloqueios de CORS ao serem renderizadas no canvas.
- Textos longos podem quebrar o layout dos templates.
- Diferenças entre sistemas operacionais podem afetar a fidelidade da imagem gerada.
- Fontes externas podem não carregar corretamente antes da exportação.
- Como a imagem local não terá recorte manual, o encaixe pode variar conforme a proporção da imagem.

## 17. Critérios de Aceite Iniciais

- O aplicativo abre diretamente na lista de layouts.
- O usuário consegue selecionar layouts por cards.
- O usuário consegue pesquisar e filtrar cards de layout.
- O usuário consegue filtrar layouts por formato e tema.
- O usuário consegue escolher entre feed 1080x1440 e story 1080x1920.
- O usuário consegue informar uma URL válida de uma notícia.
- O sistema inicia automaticamente a coleta após a URL ser informada.
- O sistema exibe indicador de carregamento durante a coleta.
- O sistema consegue coletar os principais metadados da notícia.
- O sistema exibe a mensagem definida quando a coleta falha.
- O sistema limpa o campo de URL após erro de coleta.
- O sistema consegue montar um preview com os dados coletados.
- O usuário consegue preencher todos os campos manualmente e gerar imagem sem URL.
- O usuário consegue editar manualmente `tag`, título, subtítulo e imagem.
- O usuário consegue fazer ajustes independentes por layout selecionado.
- O sistema exibe os previews em grid.
- O sistema destaca o layout selecionado para edição.
- O painel único de edição atualiza conforme o layout selecionado.
- O painel de edição pode ser recolhido.
- O usuário consegue duplicar um layout e editar a cópia de forma independente.
- O layout duplicado recebe nome automático.
- O usuário consegue remover uma instância duplicada do grid.
- O usuário consegue selecionar uma imagem local pelo explorador de arquivos.
- A imagem selecionada é encaixada no template sem recorte manual.
- O preview é atualizado após edições manuais.
- O sistema exibe erros de validação campo a campo.
- O sistema bloqueia a geração quando algum campo obrigatório está vazio.
- O sistema permite gerar mais de um formato/layout selecionado ao mesmo tempo.
- O sistema permite desmarcar um layout que não ficou adequado no preview.
- O usuário consegue gerar e baixar um arquivo PNG.
- Quando mais de uma imagem é gerada, o sistema baixa arquivos separados.
- Os arquivos são salvos na pasta padrão de downloads.
- O arquivo baixado segue a nomenclatura `{formato}-{titulo-em-slug}-{data}.png`.
- A data do arquivo segue o formato `DD-MM-YYYY`.
- O formato do arquivo usa `feed` ou `story` em minúsculo.
- O slug do título tem no máximo 80 caracteres.
- O arquivo gerado sempre está em PNG.
- O arquivo gerado respeita exatamente a resolução do formato selecionado.
- O sistema não bloqueia a geração por baixa resolução da imagem local.
- O sistema exibe a mensagem `Imagem baixada com sucesso` após baixar as imagens.
- O usuário consegue abrir a pasta de downloads após gerar as imagens.
- O sistema permite alternar entre modo claro e modo escuro.
- Templates, temas e assets podem ser configurados pelos arquivos do projeto.
- O sistema informa erro quando a URL é inválida ou quando os dados não podem ser coletados.

## 18. Referências do Professor

Orientações recebidas:

- Requisitos não funcionais não descrevem necessariamente uma funcionalidade do sistema.
- Requisitos não funcionais podem tratar de desempenho, acessibilidade, segurança, usabilidade, compatibilidade e qualidade.
- O documento deve descrever as funcionalidades, identificar quem vai usar, como vai usar e quais são os atores envolvidos.

Imagens/modelo clássico: a anexar ou descrever.

## 19. Perguntas em Aberto

1. Quais navegadores precisam ser oficialmente suportados caso exista uma versão web além do Electron?
2. O modo claro/escuro deve seguir a preferência do sistema operacional ou ser escolhido manualmente pelo usuário?
3. Quais campos opcionais cada template pode usar além de `tag`, título, subtítulo e imagem?
4. Quais temas estarão disponíveis em cada um dos 5 templates iniciais?
5. Como os templates serão organizados dentro dos arquivos do projeto?
