# Requisitos Funcionais:
Coletar metadados de link de A Gazeta;
Templates em HTML e CSS que devem ser preenchidos com esses metadados;
Usar a biblioteca [html-to-image](https://github.com/bubkoo/html-to-image) para transformar esses layouts em PNG;

# Requisitos não funcionais:
Nomenclatura da imagem gerada;
Frontend;
Seleção de cor de cada template (o mesmo template pode ter variação de cor, é importante dar a opção de seleção);
Builder de template;

# Sugestão de fluxo:
O usuário escolhe um template na lista da tela inicial;
Quando o usuário informa a URL de uma notícia, a UI coleta os metadados;
O preview é montado;
Quando o usuário clica em Criar, a UI monta a arte (template, página, campos de texto, background, tema e logo), renomeia e baixa.

# Observações:
O projeto precisa ser leve;
De preferência rodar local;
