# PH Suplementos — protótipos para apresentar no GitHub Pages

Este pacote contém uma exportação independente das telas do ERP/PDV e da loja da PH. Cada HTML já incorpora JavaScript, estilos, ícones e as imagens da marca. Não é necessário instalar Node, executar um build ou contratar banco de dados para esta apresentação.

Os dados são fictícios e ficam no navegador. O protótipo não tem login, cobrança, emissão fiscal ou comunicação com a versão privada hospedada anteriormente. Todas as pessoas que abrirem o HTML poderão acessar suas telas de demonstração. Use somente dados de teste.

## Arquivos

| Arquivo | Função |
| --- | --- |
| `index.html` | Página de abertura com botões para os dois projetos |
| `ph-erp.html` | ERP, estoque, lotes, entradas, PDV, financeiro e relatórios |
| `ph-loja.html` | Loja, catálogo, sacola e checkout simulado |
| `.nojekyll` | Informa ao GitHub Pages que o conteúdo estático já está pronto |
| `LEIA-ME.md` | Este guia de publicação e apresentação |

## Publicar os dois juntos — recomendado para amanhã

1. Extraia o ZIP no computador.
2. Crie um repositório no GitHub, por exemplo `ph-prototipo`. Em uma conta gratuita, use um repositório público para o GitHub Pages.
3. No repositório, escolha **Add file → Upload files** e envie os arquivos extraídos. Coloque `index.html`, `ph-erp.html` e `ph-loja.html` na raiz. Não envie somente o ZIP.
4. Confirme o envio em **Commit changes**.
5. Entre em **Settings → Pages**. Em **Build and deployment**, escolha **Deploy from a branch**, selecione a branch **main** e a pasta **/ (root)**, e salve.
6. Aguarde o GitHub apresentar o endereço publicado. Abra o endereço indicado pelo próprio GitHub.

Exemplo de estrutura de endereços, substituindo `SEU-USUARIO` e `ph-prototipo` pelos seus nomes:

- Abertura: `https://SEU-USUARIO.github.io/ph-prototipo/`
- ERP: `https://SEU-USUARIO.github.io/ph-prototipo/ph-erp.html`
- Loja: `https://SEU-USUARIO.github.io/ph-prototipo/ph-loja.html`

As telas internas usam `#` no endereço, como `ph-erp.html#/admin/pdv`. Isso evita erro 404 quando você atualiza uma tela no GitHub Pages. Mantenha os nomes fornecidos no pacote quando publicar tudo junto.

## Publicar em repositórios separados

Você pode enviar `ph-erp.html` para um repositório e `ph-loja.html` para outro. Em cada um, pode renomear o HTML para `index.html` e ativar Pages seguindo os passos acima. Cada arquivo funciona sozinho.

Depois abra **Opções da apresentação**, no canto inferior esquerdo, e preencha os endereços completos publicados do ERP e da loja. Clique em **Salvar links**. Isso ajusta os botões que levam de um projeto ao outro.

| Como os protótipos são abertos | Compartilham os testes? |
| --- | --- |
| Duas abas no mesmo navegador e perfil, em `https://usuario.github.io/erp/` e `https://usuario.github.io/loja/` | Sim, pois o domínio e o protocolo são os mesmos |
| Mesmo computador, mas um projeto no Chrome e outro no Edge | Não |
| Uma aba normal e outra anônima | Não |
| Computadores ou celulares diferentes | Não |
| Domínios diferentes, como `erp.exemplo.com` e `loja.exemplo.com` | Não |
| Arquivos abertos por duplo clique, sem hospedagem | O comportamento depende do navegador; não use esse modo para demonstrar o vínculo |

O compartilhamento acontece pelo armazenamento local do navegador (`localStorage`), com atualização das abas quando os dados mudam ou ao voltar para a aba. HTTPS com suporte a Web Locks coordena as gravações entre abas. Navegadores antigos ou contextos sem esse recurso devem ser usados com uma operação de cada vez.

Publicar arquivos no GitHub não cria uma API ou um banco de dados compartilhado. Para estoque real sincronizado entre computadores, funcionários e clientes, os dois sistemas precisam usar o mesmo backend autenticado e banco de dados. Os HTMLs deste pacote não se conectam automaticamente ao banco da versão privada anterior.

## Leitor USB / Bluetooth e código de barras

O protótipo recebe o leitor como um teclado. O computador reconhece o dispositivo; a página recebe as teclas enviadas. Ela não detecta a porta USB, não solicita WebUSB e não confirma a conexão física.

- Configure o leitor em **USB HID / Keyboard Wedge**, ou modo teclado no Bluetooth.
- Configure o terminador/sufixo **Enter**. Para o protótipo, evite prefixos e caracteres extras.
- Leitores configurados como porta serial/COM ou que dependem de SDK próprio precisam de outra integração.
- Teste primeiro no Bloco de Notas: ao bipar, devem aparecer os números e, normalmente, uma quebra de linha.
- No HTML, **Opções da apresentação → Testar leitor sem cadastrar produto** também permite conferir os números recebidos.
- A leitura automática do HTML aceita códigos numéricos de 8 a 14 dígitos, preserva zeros iniciais e usa intervalo máximo de 80 ms entre caracteres para reconhecer a sequência rápida. O modelo físico ainda precisa ser testado no seu computador.

### Cadastro na tela mostrada

1. Em **Produtos → Novo produto**, clique em **Código de barras (GTIN)**.
2. Bipe a embalagem. Os números devem aparecer no campo.
3. Preencha nome, marca, variação, tamanho, preço e custo. O código não consulta uma base externa e não preenche esses dados sozinho.
4. Clique em **Cadastrar produto**. Nos HTMLs exportados, o Enter do leitor move o foco para Marca e não envia o formulário antes da conferência.

Cada código identifica uma variação do produto. Uma embalagem com outro GTIN deve corresponder ao cadastro certo. O GTIN comum não informa a quantidade em estoque, o lote ou a validade: eles são registrados na entrada.

### Entrada e venda

- Em **Entrada de mercadoria**, com a tela ativa e fora dos campos de edição, bipe o produto. Se o código já existir, abre a conferência do lote. Se não existir, aparece o fluxo para cadastrar.
- Informe lote, validade, quantidade e custo; confirme a entrada. Cadastrar o produto sozinho não cria saldo de estoque.
- No **PDV**, abra o caixa e bipe um produto com o mesmo GTIN cadastrado. É necessário ter saldo vendável. Lotes vencidos ou bloqueados não podem ser vendidos.
- As telas de inventário e transferência mantêm os controles de seleção da versão anterior; este pacote não acrescenta um fluxo completo de bipagem nessas telas.

## Roteiro de apresentação — cerca de 5 a 10 minutos

1. Abra o ERP e a loja em duas abas do **mesmo navegador e perfil**, pelos links HTTPS publicados.
2. No ERP, mostre **Visão geral**, os depósitos e **Controle de validade**.
3. Cadastre um produto de teste usando o código de uma embalagem disponível. O número pode ser real para testar o leitor; use os demais dados apenas como exemplo. Cada GTIN deve ser único no cadastro.
4. Em **Entrada de mercadoria**, registre 3 unidades na **Loja principal**, com lote de exemplo e validade pelo menos 30 dias à frente. Essa escolha evita os avisos críticos durante a demonstração inicial. A loja online desta versão consulta a Loja principal.
5. Em **Produtos → Editar**, altere **Na loja online** de Rascunho para **Publicado** e salve.
6. Volte à aba da loja, pesquise o produto e confira a disponibilidade. Se necessário, atualize a página.
7. Coloque 1 unidade na sacola e conclua o checkout simulado. Não há pagamento real.
8. Volte ao ERP: confira o pedido, a saída de estoque e o lançamento financeiro.
9. Abra o caixa no PDV, bipe o produto e simule outra venda. Confira o saldo final.
10. Para demonstrar os alertas, use os lotes fictícios já existentes com validade próxima, crítica, vencida e bloqueada.

Se preferir testar sem leitor, digite o GTIN ou selecione o produto pela busca. Digitar no campo GTIN cadastra o mesmo código que o leitor enviaria.

## Se algo não funcionar

| Situação | Conferência |
| --- | --- |
| Nada aparece ao bipar | Teste no Bloco de Notas e confira modo HID, conexão e configuração do leitor |
| Código aparece, mas não é encontrado | Confira se o GTIN cadastrado corresponde exatamente ao código lido, incluindo zeros iniciais |
| Produto cadastrado, mas sem estoque | Registre a entrada por lote; o cadastro não adiciona quantidade |
| Produto não aparece na loja | Confira se está Publicado; produtos novos começam como Rascunho |
| Disponibilidade não acompanha o ERP | Use a Loja principal, o mesmo navegador/perfil e o mesmo domínio; atualize a aba |
| Produto indisponível apesar de saldo | Confira validade, bloqueios, reservas na sacola e exigência de autorização para lote crítico |
| GitHub mostra arquivos, mas não o site | Ative Settings → Pages; subir o repositório sozinho não ativa a publicação |
| Erro 404 | Confira a pasta configurada em Pages, o nome do arquivo e se o endereço aponta para ele |
| Dados locais não podem ser gravados | Abra em uma aba normal e permita armazenamento de sites |

Em **Opções da apresentação**, há uma opção para salvar uma cópia JSON dos dados de teste e outra para restaurar a demonstração. Restaurar apaga os testes locais compartilhados pelos dois HTMLs e volta aos exemplos iniciais. Limpar os dados do navegador também remove os testes. O arquivo JSON é uma cópia para consulta; esta versão não oferece importação dessa cópia pela interface.

## O que foi verificado nesta exportação

- Geração de dois HTMLs independentes, com recursos incorporados e sem dependências de servidor no pacote.
- TypeScript e sintaxe JavaScript.
- Cinco testes automatizados: sequência do leitor, cadastro/entrada/publicação/compra/baixa no ERP, idempotência e rejeição de operação inválida, gravações sequenciais e navegação em subpastas/repositórios.
- A exportação preserva as limitações funcionais informadas na versão anterior. Não transforma o protótipo em sistema de produção.
- O leitor físico e a publicação na sua conta GitHub não foram testados aqui. Faça o roteiro acima antes da reunião.

## Referências

- GitHub Pages — criar um site: https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site
- GitHub Pages — configurar a origem da publicação: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
- MDN — armazenamento local e restrição por origem: https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage

Preparado em 07/09/2026.
