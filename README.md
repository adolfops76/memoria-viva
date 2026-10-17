# Memória Viva

Aplicação web pessoal para captura, organização, busca, conexão e revisitação de conhecimento. A versão 1.0 roda como site estático no GitHub Pages e não envia registros para o servidor.

## Usar

Abra o site e use **Capturar** ou a caixa “O que você descobriu hoje?”. Os registros são guardados no armazenamento local do navegador usado. Para transportar dados, abra **Dados e ajustes → Backup e restauração** e exporte/importa o arquivo JSON. Também há exportação CSV e Markdown.

> O armazenamento local não sincroniza entre dispositivos e pode ser apagado ao limpar os dados do navegador. Mantenha backups JSON em local privado.

## Privacidade

O repositório e o site são públicos. Nenhum registro de pesquisa, título, URL, índice privado, documento, chave ou token é incluído no código publicado. A V1 não autentica nem sincroniza com Google Drive. É possível registrar um link privado do Drive manualmente; a permissão continua sendo controlada pelo Drive. O site não afirma preservar páginas automaticamente. Para preservação, salve a página (por exemplo, usando SingleFile), exporte PDF/Markdown quando aplicável e guarde o arquivo na sua conta do Drive com acesso restrito; registre o link no cadastro.

Não coloque documentos privados, dados de pesquisa ou segredos neste repositório.

## Funcionalidades da V1

- Dashboard com captura rápida, contadores, recentes e fila de revisão.
- Cadastro e edição de fontes/conhecimentos com distinção entre descrição original e comentários pessoais.
- Biblioteca com busca, filtros e ordenação.
- Revisitação espaçada configurável; revisar, adiar, aprofundar, dominar e arquivar por edição do status.
- Mapa visual interativo com ligações derivadas de assunto e etiquetas em comum.
- Projetos com hierarquia numérica.
- Tema claro/escuro, layout responsivo para desktop, tablet e celular.
- Backup/restauração JSON e exportações CSV/Markdown.

## Pendências

- Login e sincronização autenticada com Google Drive (OAuth 2.0) e verificação de pastas existentes.
- Persistência multiaparelho e cópias de segurança automáticas.
- Captura automatizada de páginas, extração de texto e gestão de snapshots HTML/PDF/imagens. Na V1, a preservação é manual; não se declara cópia salva sem ação do usuário.
- Histórico de alterações completo, conexões editáveis entre conceitos/projetos e classificação/resumos assistidos por IA.
- Migração futura para React/TypeScript e testes automatizados integrados.

## Arquitetura

`index.html` é um app estático sem backend; GitHub Pages entrega os arquivos públicos. `localStorage` mantém os dados apenas no navegador local. O GitHub Actions publica o conteúdo da branch `main` com Pages. Para sincronização privada futura, adicione um backend com autenticação e armazenamento privado ou integração OAuth do Google Drive; nunca coloque credenciais de serviço no front-end público.

## Desenvolvimento e publicação

A versão atual não exige build ou dependências. Teste localmente abrindo `index.html` ou rode `python -m http.server 8000`. Alterações enviadas à branch `main` serão publicadas pela workflow em `.github/workflows/pages.yml`.
