# PRD — CineSI

**Product Requirements Document**

---

## 1. Identificação

| Campo | Valor |
|---|---|
| Projeto | CineSI — catálogo pessoal de filmes e séries |
| Autor | Douglas Henrick |
| Disciplina | TSI32B — Desenvolvimento de Páginas Web com Framework e CSS |
| Professor | Prof. Dr. Roni Fabio Banaszewski |
| Instituição | UTFPR — Campus Guarapuava |
| Versão | 1.0 |
| Data | 06/09/2026 |

## 2. Descrição

### 2.1 Problema

Quem consome muito conteúdo audiovisual perde o controle do próprio histórico. A informação fica espalhada entre prints no celular, notas soltas, listas de plataformas diferentes e memória. Três perguntas ficam sem resposta fácil:

- O que eu já assisti e o que eu achei?
- O que eu decidi assistir e ainda não assisti?
- Onde foi parar aquele título que alguém recomendou semana passada?

As plataformas de streaming resolvem isso apenas dentro do próprio catálogo. Não existe um lugar único, independente de serviço, para registrar esse histórico.

### 2.2 Propósito do sistema

O CineSI é uma aplicação web responsiva que permite buscar filmes e séries em uma base pública, salvar títulos em listas pessoais com status e avaliação, e consultar esse histórico depois.

O sistema não recomenda conteúdo nem substitui plataformas de streaming. Ele registra e organiza.

### 2.3 Escopo

**Dentro do escopo (MVP)**

- Busca de filmes e séries em API pública, com resultados em cards.
- Cadastro de um título na coleção pessoal, com status, nota, data e comentário.
- Listagem da coleção com filtro por status e por lista.
- Edição e exclusão de itens da coleção.
- Página de detalhes de um título.
- Página de perfil com dados de contato validados.
- Persistência das preferências de navegação no navegador.

**Fora do escopo**

- Autenticação real e contas de múltiplos usuários.
- Reprodução de conteúdo ou integração com plataformas de streaming.
- Algoritmo de recomendação.
- Rede social, comentários públicos ou compartilhamento entre usuários.
- Aplicativo mobile nativo.

## 3. Atores do Sistema

| Ator | Descrição | Permissões |
|---|---|---|
| **Visitante** | Pessoa que acessa a aplicação sem ter registrado dados próprios. Consulta o catálogo público, mas não mantém coleção. | Navegar pela home, buscar títulos, visualizar detalhes vindos da API pública. |
| **Colecionador** | Ator principal. Pessoa que mantém a própria coleção de títulos assistidos e por assistir. | Tudo do Visitante, mais: criar, consultar, editar e excluir títulos da coleção; gerenciar listas; manter os dados do perfil. |

**Nota sobre a distinção.** A aplicação é monousuária e não possui autenticação — decisão registrada em *Fora do escopo*. A separação entre os dois atores é funcional, refletindo quais áreas do sistema operam sobre dados pessoais e quais operam apenas sobre o catálogo público. Ela não é imposta por um mecanismo de login.

**Perfil de referência do Colecionador**

Marina, 24 anos, estudante de graduação. Assina duas plataformas de streaming e acompanha recomendações de amigos e de redes sociais. Acumula uma lista mental de "preciso ver isso" que nunca vira ação, porque não está anotada em lugar nenhum. Quando termina uma série, gosta de registrar uma nota e um comentário curto para lembrar da impressão meses depois. Usa o celular na maior parte do tempo e o notebook quando está em casa.

## 4. Histórias de Usuário (Escopo)

**US01 — Buscar títulos**
Como **Visitante**, eu quero buscar um filme ou série pelo nome, para que eu encontre o título sem precisar digitar os dados manualmente.

*Critérios de aceite:*
- A busca dispara a partir de 3 caracteres.
- Os resultados exibem pôster, título, tipo (filme/série) e ano.
- Busca sem resultados exibe mensagem explicativa, não uma tela vazia.
- Falha de rede exibe mensagem de erro e opção de tentar novamente.

---

**US02 — Ver detalhes de um título**
Como **Visitante**, eu quero abrir os detalhes de um título, para que eu decida se vale a pena adicioná-lo à minha lista.

*Critérios de aceite:*
- Exibe sinopse, gêneros, ano e imagem em resolução maior.
- Se o título já estiver na coleção, exibe também status, nota, data e comentário registrados.

---

**US03 — Salvar um título na coleção**
Como **Colecionador**, eu quero salvar um título encontrado na busca, para que eu não perca a referência.

*Critérios de aceite:*
- O formulário vem pré-preenchido com os dados vindos da API.
- Status é obrigatório na inclusão.
- Um título já presente na coleção não pode ser incluído novamente (RN01).
- Após salvar, o usuário é levado à listagem com o item visível.

---

**US04 — Consultar minha coleção**
Como **Colecionador**, eu quero ver todos os títulos salvos em uma listagem, para que eu tenha a visão geral do meu histórico.

*Critérios de aceite:*
- Exibição em cards no mobile e em tabela ou grade no desktop.
- Filtro por status e por lista.
- Coleção vazia exibe estado inicial com instrução de como começar.

---

**US05 — Atualizar um título**
Como **Colecionador**, eu quero editar o status, a nota e o comentário de um título, para que o registro reflita que já assisti ou que mudei de opinião.

*Critérios de aceite:*
- A edição abre com os valores atuais carregados.
- As regras RN03 e RN04 são aplicadas na validação.
- A data de última atualização é registrada.

---

**US06 — Remover um título**
Como **Colecionador**, eu quero excluir um título da coleção, para que a lista permaneça relevante.

*Critérios de aceite:*
- A exclusão exige confirmação em modal (RN07).
- Após confirmar, o item some da listagem sem recarregar a página.

---

**US07 — Organizar títulos em listas**
Como **Colecionador**, eu quero agrupar meus títulos em listas nomeadas, para que eu separe contextos diferentes de consumo.

*Critérios de aceite:*
- É possível criar uma lista informando nome e cor.
- Todo título salvo pertence a exatamente uma lista (RN06).
- Uma lista com títulos não pode ser excluída diretamente (RN10).

---

**US08 — Manter meus dados de contato**
Como **Colecionador**, eu quero registrar meu nome, e-mail e telefone no perfil, para que a aplicação seja personalizada com meus dados.

*Critérios de aceite:*
- E-mail e telefone validados por expressão regular (RN08).
- Mensagens de erro exibidas por campo, não em bloco único.
- Telefone aceito no formato brasileiro com DDD.

---

**US09 — Manter minhas preferências entre visitas**
Como **Colecionador**, eu quero que a aplicação lembre do último filtro que usei, para que eu não precise reconfigurar tudo a cada acesso.

*Critérios de aceite:*
- O filtro selecionado é gravado no navegador.
- Ao reabrir a aplicação, o filtro anterior é restaurado.

## 5. Regras de Negócio

| ID | Regra |
|---|---|
| RN01 | Um mesmo título não pode ser salvo duas vezes na coleção. O identificador da API pública é a chave natural de unicidade. |
| RN02 | Os status permitidos são: `quero_assistir`, `assistindo`, `concluido`. Nenhum outro valor é aceito. |
| RN03 | A nota só pode ser informada quando o status for `concluido`. É um inteiro entre 0 e 10. |
| RN04 | A data assistida é obrigatória quando o status for `concluido` e não pode ser posterior à data atual. |
| RN05 | O comentário é opcional e limitado a 280 caracteres. |
| RN06 | Todo título salvo deve estar associado a exatamente uma lista. |
| RN07 | Exclusões exigem confirmação explícita do usuário antes de serem efetivadas. |
| RN08 | E-mail e telefone do perfil são validados por expressão regular antes do envio. |
| RN09 | Toda falha de comunicação com a API deve resultar em mensagem visível ao usuário. A aplicação nunca falha em silêncio. |
| RN10 | Uma lista que contenha títulos não pode ser excluída sem que os títulos sejam realocados ou removidos antes. |

## 6. Requisitos não funcionais

| Categoria | Requisito |
|---|---|
| Responsividade | Layout funcional de 320px a 1920px, construído mobile first. |
| Acessibilidade | Labels associados aos campos, texto alternativo nas imagens, contraste mínimo AA. |
| Compatibilidade | Navegadores modernos com suporte a ES6+ e `fetch`. |
| Hospedagem | Site estático no GitHub Pages, sem etapa de build. Dependências via CDN. |
| Desempenho | Imagens carregadas em resolução adequada ao viewport. |
| Manutenibilidade | Código organizado em módulos por responsabilidade, com linter e formatador configurados. |

## 7. Rastreabilidade — Histórias de Usuário × Indicadores de Desempenho

| História | IDs atendidos |
|---|---|
| US01 — Buscar títulos | ID 24 |
| US02 — Ver detalhes | ID 09, ID 10 |
| US03 — Salvar título | ID 11, ID 13, ID 22 |
| US04 — Consultar coleção | ID 04, ID 23 |
| US05 — Atualizar título | ID 11, ID 22 |
| US06 — Remover título | ID 04, ID 20 |
| US07 — Organizar em listas | ID 13, ID 22, ID 23 |
| US08 — Dados de contato | ID 11, ID 12, ID 21 |
| US09 — Preferências | ID 14 |

Os demais indicadores (ID 01–08, 15–19) são atendidos por decisões de projeto e de processo, documentadas em `architecture.md`.

## 8. Histórico de revisões

| Versão | Data | Descrição |
|---|---|---|
| 1.0 | 06/09/2026 | Versão inicial — Atividade 03 |
