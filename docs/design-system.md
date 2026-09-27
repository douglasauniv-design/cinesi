# 🎨 Design System - CineSI

Neste projeto, partimos de um framework UI e aplicamos customizações para refletir a identidade visual extraída do protótipo construído no Stitch.

### 1. Framework Base

- **Framework escolhido:** Bootstrap 5 (`v5.3.8`)
- **Motivação:** A interface do CineSI é construída sobre um tema escuro, e o Bootstrap 5 oferece suporte nativo a esse modo através do atributo `data-bs-theme="dark"` e de variáveis CSS sobrescrevíveis. O MaterializeCSS impõe as superfícies claras do Material Design como padrão, o que exigiria customização mais agressiva para chegar ao mesmo resultado.

### 2. Paleta de Cores (Customização)

A paleta foi construída a partir de uma decisão central: os pôsteres dos filmes precisam ser o elemento mais luminoso da tela. Todas as superfícies da interface são escuras justamente para que a atenção do usuário caia sobre o conteúdo, e não sobre os controles.

- **Cor Primária (Ação):** `#F5A524` *(Âmbar)*
  - *Uso:* Botões principais, links, chips ativos, ícone de nota e o segmento "SI" da marca. Remete ao letreiro iluminado de marquise de cinema. Foi escolhido âmbar em vez do vermelho tradicional do cinema para não competir semanticamente com a cor de erro nos formulários.
- **Cor de Fundo (Background):** `#0F1115` *(Quase preto, com viés azulado)*
  - *Uso:* Fundo de todas as páginas e do rodapé.
- **Cor de Superfície:** `#1A1D24`
  - *Uso:* Cards, navbar e campos de formulário. O contraste com o fundo é o que separa os elementos, dispensando sombras pesadas.
- **Cor de Superfície Elevada:** `#262A34`
  - *Uso:* Modais e menus suspensos, que precisam se destacar da camada abaixo.
- **Cor de Erro:** `#E5484D` *(Vermelho)*
  - *Uso:* Bordas e mensagens de campos inválidos, ícone de alerta e o botão destrutivo do modal de exclusão.

**Cores semânticas de status.** O sistema de status é o núcleo da regra de negócio, então cada estado recebe cor própria, com função e não decoração:

- **Quero assistir:** `#F5A524` *(Âmbar)* — mesma cor da ação primária, porque representa intenção.
- **Assistindo:** `#7C5CFF` *(Violeta)* — em progresso.
- **Concluído:** `#30A46C` *(Verde)* — encerrado e passível de avaliação.

**Cores de texto.** Texto principal em `#ECEDEE` e texto secundário em `#9BA1A6`, usado em metadados como ano, gênero e contadores.

### 3. Tipografia

Importada via Google Fonts para substituir a fonte padrão do framework:

- **Títulos (H1 a H6) e a marca:** `Poppins, sans-serif` (Peso: 600).
- **Textos corridos, campos de formulário e metadados:** `Inter, sans-serif` (Pesos: 400 e 500).

A escala aplicada é de 32px para título de tela no desktop e 24px no mobile, 20px para título de seção, 16px para corpo e 14px para legendas e metadados. A variação entre desktop e mobile no título de tela será implementada com `clamp()` e unidades relativas, atendendo à tipografia fluida.

### 4. Diretrizes de Uso de Componentes

Regras para aplicação dos componentes do framework dentro da identidade do CineSI. Os raios de borda seguem três valores fixos: 12px em cards e imagens, 8px em botões e campos, e formato pílula em chips e badges.

- **Navbar (`.navbar`):** Fixa no topo, altura de 64px, fundo na cor de superfície. Colapsa em menu hambúrguer no breakpoint mobile. É um dos componentes marcados para substituição pelo componente pronto do framework.
- **Cards (`.card`):** Usados obrigatoriamente para exibir títulos na busca, na coleção e nos carrosséis. O pôster ocupa o topo em proporção 2:3 com `object-fit: cover`, e os metadados ficam abaixo com 16px de respiro interno.
- **Modais (`.modal`):** Reservados para duas situações — o formulário de inclusão e edição de um título, e a confirmação de exclusão. Nenhuma exclusão ocorre sem passar por um modal.
- **Carrossel (`.carousel`):** Usado apenas na página inicial, para as seções de destaques e de títulos em andamento.
- **Botões (`.btn`):** Ações principais usam preenchimento âmbar com texto escuro. Ações secundárias e de cancelamento usam apenas contorno. Ações destrutivas usam a cor de erro, e quando aparecem fora de um modal são discretas, no formato de botão de texto.
- **Badges de status (`.badge`):** Sempre em formato pílula, posicionados sobre o canto do pôster, coloridos conforme a cor semântica do status correspondente.
- **Formulários (`.form-control`):** Campos com 48px de altura nas telas e 40px dentro de modais. Estados de validação são comunicados pela borda — vermelha para erro, verde para válido — acompanhados de ícone interno à direita e mensagem abaixo do campo.
