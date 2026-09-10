# 📄 Product Requirements Document (PRD) - CineSI

**Autor:** Douglas Henrick

## 1. Visão Geral e Objetivo

O **CineSI** é uma aplicação web para catalogar filmes e séries de forma pessoal. O usuário busca títulos em uma base pública de cinema, salva os que lhe interessam em listas próprias e registra o que achou de cada um após assistir.

**O problema que resolve:** quem consome muito conteúdo audiovisual perde o controle do próprio histórico. As recomendações chegam por vários canais e ficam espalhadas entre prints, anotações soltas e memória. As plataformas de streaming organizam apenas o próprio catálogo, e nenhuma delas responde "o que eu já assisti e o que eu achei".

**A regra de negócio principal:** o sistema separa **intenção** de **histórico**. Todo título salvo carrega obrigatoriamente um status (`quero assistir`, `assistindo` ou `concluído`), e os campos de avaliação — nota e data — só são aceitos quando o título está concluído. Não é possível avaliar aquilo que ainda não se assistiu.

## 2. Atores do Sistema

- **Visitante:** usuário que acessa a aplicação para consultar o catálogo público. Busca títulos e visualiza detalhes, mas não mantém coleção própria.
- **Colecionador:** ator principal. Mantém sua coleção pessoal de títulos, organizando-os em listas, atribuindo status, notas e comentários.
- **O Catálogo (Sistema):** ator invisível representado pela API pública do TMDB. Fornece os dados de cada título — nome, pôster, sinopse, ano e gêneros — evitando que o Colecionador precise digitá-los manualmente.

## 3. Histórias de Usuário e Escopo

Abaixo estão as funcionalidades principais do MVP (Minimum Viable Product), escritas sob a perspectiva do usuário final.

### 🔍 Épico 1: Descoberta de Títulos

- **US01 - Buscar Títulos:** Como um Visitante, quero buscar um filme ou série pelo nome, para encontrar o título sem precisar digitar seus dados manualmente.
  - *Critérios de Aceitação:* A busca dispara a partir de 3 caracteres; os resultados exibem pôster, título, tipo e ano; busca sem resultados exibe mensagem explicativa; falha de rede exibe mensagem de erro com opção de tentar novamente.
- **US02 - Visualizar Detalhes:** Como um Visitante, quero abrir os detalhes de um título, para decidir se vale a pena adicioná-lo à minha coleção.
  - *Critérios de Aceitação:* Exibe sinopse, gêneros, ano e imagem em resolução maior; se o título já estiver na coleção, exibe também o status, a nota e o comentário registrados.

### 🎬 Épico 2: Gestão da Coleção

- **US03 - Adicionar Título:** Como um Colecionador, quero salvar um título encontrado na busca, para não perder a referência.
  - *Critérios de Aceitação:* O formulário vem pré-preenchido com os dados vindos do Catálogo; o status é obrigatório; um título já presente na coleção não pode ser incluído novamente; após salvar, o usuário é levado à listagem com o item visível.
- **US04 - Consultar Coleção:** Como um Colecionador, quero ver todos os títulos salvos em uma listagem, para ter a visão geral do meu histórico.
  - *Critérios de Aceitação:* Exibição em cards no mobile e em grade no desktop; filtro por status e por lista; coleção vazia exibe estado inicial com instrução de como começar.
- **US05 - Avaliar e Atualizar:** Como um Colecionador, quero editar o status, a nota e o comentário de um título, para registrar que já assisti ou que mudei de opinião.
  - *Critérios de Aceitação:* A edição abre com os valores atuais carregados; a nota (0 a 10) só é aceita quando o status for "concluído"; a data assistida é obrigatória nesse status e não pode ser futura; o comentário é limitado a 280 caracteres.
- **US06 - Remover Título:** Como um Colecionador, quero excluir um título da coleção, para manter a lista relevante.
  - *Critérios de Aceitação:* A exclusão exige confirmação em modal; após confirmar, o item some da listagem sem recarregar a página.
- **US07 - Organizar em Listas:** Como um Colecionador, quero agrupar meus títulos em listas nomeadas, para separar contextos diferentes de consumo.
  - *Critérios de Aceitação:* É possível criar uma lista informando nome e cor; todo título pertence a exatamente uma lista; uma lista que contenha títulos não pode ser excluída antes que eles sejam realocados ou removidos.

### 👤 Épico 3: Perfil e Preferências

- **US08 - Manter Perfil:** Como um Colecionador, quero registrar meu nome, e-mail e telefone, para personalizar a aplicação com meus dados.
  - *Critérios de Aceitação:* E-mail e telefone validados por expressão regular (REGEX); mensagens de erro exibidas por campo; telefone aceito no formato brasileiro com DDD.
- **US09 - Preservar Preferências:** Como um Colecionador, quero que a aplicação lembre do último filtro que usei, para não precisar reconfigurar tudo a cada acesso.
  - *Critérios de Aceitação:* O filtro selecionado é gravado no navegador via Web Storage; ao reabrir a aplicação, o filtro anterior é restaurado.
