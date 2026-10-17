# Memória Viva

Aplicação web pessoal para captura, organização, busca, conexão e revisitação de conhecimento. O site é estático no GitHub Pages. Os registros ficam localmente até que o usuário escolha salvá-los ou restaurá-los no Google Drive.

## Usar

Abra o site e use **Capturar** ou a caixa “O que você descobriu hoje?”. Para backup entre aparelhos, abra **Dados e ajustes → Google Drive**, configure OAuth, conecte a conta, selecione a pasta privada `4. Índice de Conhecimento` e use **Salvar backup no Drive** ou **Baixar índice do Drive**. A sincronização é manual; evite salvar em paralelo a partir de cópias locais diferentes.

Também há exportação/restauração JSON e exportações CSV/Markdown.

## Configurar o Google Drive

1. No [Google Cloud Console](https://console.cloud.google.com/), crie ou selecione um projeto.
2. Ative **Google Drive API** e **Google Picker API**.
3. Configure a tela de consentimento OAuth e crie um **OAuth Client ID para aplicativo Web**. Em **Authorized JavaScript origins**, adicione `https://adolfops76.github.io`.
4. Crie uma chave de API. Restrinja o uso por HTTP referrer ao site `https://adolfops76.github.io/*` e ao frame do Picker `https://docs.google.com/*`; restrinja as APIs permitidas à Google Picker API e Google Drive API.
5. Copie o OAuth Client ID, a chave e o número do projeto Google Cloud para **Dados e ajustes → Google Drive** e salve a configuração neste navegador.
6. Clique **Conectar Google**, autorize o escopo `drive.file`, selecione a pasta privada `4. Índice de Conhecimento` e salve o backup.

O site cria ou atualiza nessa pasta o arquivo privado `MemoriaViva-index.json`. Para usar outro aparelho, repita a configuração OAuth, conecte a mesma conta, selecione a mesma pasta e baixe o índice. O arquivo substitui os dados locais somente após confirmação. O token OAuth fica em memória durante a sessão e não é salvo no `localStorage` nem no repositório. Client ID, chave de API e número do projeto são configuração pública do cliente, guardada apenas no navegador e protegida pelas restrições indicadas; não use chave de serviço nem segredo OAuth no front-end.

A conexão do site não envia automaticamente os arquivos originais das fontes. Faça a captura da página (por exemplo, com SingleFile), salve HTML/PDF/Markdown e imagens importantes no Drive privado, depois registre o link no conhecimento. O site não afirma que uma fonte foi preservada sem você salvar o arquivo.

## Privacidade e limites

O repositório e o site são públicos. Nenhum registro, título, URL privada, ID de pasta, Client ID, chave ou token está fixado no código. Ao clicar para salvar, os dados do seu índice são enviados à pasta do Drive que você selecionou; as permissões dessa pasta controlam quem pode vê-los. O escopo OAuth usado é `drive.file`, para arquivos criados ou escolhidos pelo usuário para o app.

O armazenamento local não sincroniza por si só e pode ser apagado ao limpar os dados do navegador. Mantenha uma cópia no Drive. A sincronização atual é manual, sem mesclagem automática ou prevenção de conflitos entre aparelhos.

Não coloque documentos privados, registros ou segredos no repositório público.

## Funcionalidades

- Dashboard com captura rápida, contadores, capturas recentes e fila de revisão.
- Cadastro e edição com distinção entre descrição original e comentários pessoais.
- Biblioteca com busca, filtros e ordenação.
- Revisitação espaçada configurável; revisar, adiar, aprofundar, dominar e arquivar.
- Mapa de conexões baseado em assuntos e etiquetas em comum.
- Projetos com hierarquia numérica.
- Tema claro/escuro, layout responsivo, backup/restauração JSON e exportações CSV/Markdown.
- Backup JSON privado no Drive por ação explícita e restauração em outro navegador.

## Pendências

- Testar a autorização OAuth e o fluxo de Picker com as credenciais do projeto Google Cloud do proprietário.
- Sincronização automática, mesclagem de alterações e prevenção de conflitos.
- Upload automatizado de fontes originais e captura de páginas.
- Histórico completo de alterações, conexões editáveis e classificação/resumos assistidos por IA.
- Migração futura para React/TypeScript e testes automatizados integrados.

## Arquitetura e publicação

`index.html` é um app estático sem backend; GitHub Pages entrega os arquivos públicos. `localStorage` guarda os dados locais. A integração OAuth usa o Google Identity Services e chamadas diretas à Drive API a partir do navegador; o Picker permite ao usuário escolher a pasta. Tokens nunca são gravados. O GitHub Actions publica a branch `main` usando `.github/workflows/pages.yml`.

A versão atual não exige build ou dependências. Para testar localmente, abra `index.html` ou rode `python -m http.server 8000`. OAuth precisa de uma origem autorizada com HTTPS, como o endereço publicado no GitHub Pages.
