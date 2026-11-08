# MiniProj1 – Currículo em Single Page Application (Vue.js)

Miniprojeto da Tarefa 2.2 da unidade curricular **Programação Web Avançada** (Mestrado em Engenharia Informática e Tecnologia Web, Universidade Aberta).

**Autor:** José Ernesto Constantino Bule

## Descrição

Apresenta o currículo pessoal construído como uma *Single Page Application* (SPA). Todo o site está num único ficheiro, `index.html`, carregado uma só vez pelo navegador. A navegação entre secções é feita por links internos e janelas modais, sem recarregar a página.

Secções:

- **Início**: faz uma apresentação breve e atalhos para as restantes secções
- **Quem Sou Eu?**: aqui faz-se uma apresentação pessoal e dados principais
- **O que faço?**: nesta secção apresentam-se áreas de atividade, com detalhe em janela modal
- **Hobbies**: nesta última secção é onde apresenta os hobbies, também com detalhe em janela modal

O cabeçalho com o menu e o rodapé com os contactos das redes sociais (identidade virtual) estão presentes em todas as vistas.

## Tecnologias

- HTML5 e CSS3 (layout responsivo com Flexbox e CSS Grid)
- [Vue.js 3](https://vuejs.org/) com a *Options API*: componentes, dados reativos, propriedades calculadas e diretivas
- [Vue Router 4](https://router.vuejs.org/) em modo *hash* (`index.html#/quem-sou-eu`), com rotas nomeadas
- [Font Awesome 6](https://fontawesome.com/): contactos das redes sociais

As bibliotecas são carregadas por CDN, por isso não é preciso instalar nada.

## Como executar

1. Descarregar ou clonar o repositório:
   ```
   git clone https://github.com/ernestobule-rgb/MiniProj1.git
   ```
2. Abrir o ficheiro `index.html` num navegador (Chrome ou Firefox), com ligação à Internet.

## Estrutura

```
MiniProj1/
├── index.html                          # SPA completa (HTML, CSS e JavaScript)
├── README.md                           # descrição do projeto
├── .gitattributes                      # normaliza os fins de linha (LF)
├── img/
│   ├── foto.jpg                        # fotografia de perfil
│   ├── hobby-animacao.jpg              # imagem do hobby "Assistir filmes e séries animadas"
│   ├── hobby-passear.jpg               # imagem do hobby "Passear"
│   └── hobby-jogos.jpg                 # imagem do hobby "Jogar videojogos"
└── wireframes/
    ├── Wireframes MiniProj1.drawio     # wireframes editáveis (draw.io), 8 vistas
    ├── Wireframes MiniProj1.pdf        # wireframes exportados em PDF
    └── wireframes.html                 # fonte HTML da primeira versão dos wireframes
```

## Organização do código

- **Dados**: todo o conteúdo do currículo está no objeto `cv`, no início do `<script>`. 
- **Vistas**: uma por secção (`PaginaInicio`, `PaginaQuemSou`, `PaginaOQueFaco`, `PaginaHobbies`), ligadas a rotas nomeadas.
- **Componentes reutilizáveis**: `ListaCartoes`, `CartaoItem` e `JanelaModal`. Recebem dados do pai por `props` e comunicam com o pai apenas através de eventos (`$emit`).
- **Janela modal**: fecha com o botão ×, com o botão Fechar, com a tecla Esc ou com um clique fora da janela.

## Ligação ao capítulo 3 do livro recomendado

O projeto aplica os conceitos do capítulo 3 de Queirós e Portela (2020). 

| Conceito do livro | Onde é usado no projeto |
| --- | --- |
| Inclusão do Vue por CDN | `<script>` no `<head>` |
| Instância com `data`, `methods` e elemento raiz | instância principal (`#app`) |
| Funções do ciclo de vida | `mounted`/`beforeUnmount` (botão "voltar ao topo"); `mounted` da `JanelaModal` |
| Interpolação e abreviações `:` e `@` | todos os *templates* |
| Propriedades calculadas | `nomeCurto`, `anoAtual`, `numero` |
| Interligação de classes e estilos | `:class="{ aberto: menuAberto }"`, `:style` na fotografia |
| `v-if`/`v-else` e `v-show` | fotografia ou iniciais; botão "voltar ao topo" |
| `v-for` com índice | numeração dos cartões (01, 02, 03) |
| Modificadores de eventos e de teclas | `@click.self` e `@keyup.esc` na janela modal |
| Registo global e local de componentes | `app.component(...)` e `components: { JanelaModal }` |
| Comunicação pai–filho com `props` e `$emit` | `ListaCartoes` → `CartaoItem` → evento `selecionar` |
| `router-link`, `router-view` e modo *hash* | menu, cartões do Início e `<main>` |
| Navegação programática (`router.push`) | botão "Conhecer-me" |
| Rotas nomeadas | `:to="{ name: 'hobbies' }"` |
| Redirecionamentos | rota desconhecida → Início |
| Guia de estilo: nomes compostos, `data` como função, `props` tipadas, `:key` | todos os componentes |

### Versão do Vue

O livro usa o Vue 2.6. O projeto usa o **Vue 3** com a mesma *Options API* (`data`, `methods`, `computed`, funções do ciclo de vida), porque o Vue 2 deixou de ter suporte no final de 2023. As diferenças de sintaxe são poucas:

| Livro (Vue 2) | Projeto (Vue 3) |
| --- | --- |
| `new Vue({ el: '#app', ... })` | `createApp({ ... }).mount('#app')` |
| `Vue.component('nome', { ... })` | `app.component('Nome', { ... })` |
| `new VueRouter({ mode: 'hash', routes })` | `createRouter({ history: createWebHashHistory(), routes })` |
| `{ path: '*', redirect: '/' }` | `{ path: '/:pathMatch(.*)*', redirect: { name: 'inicio' } }` |
| `beforeDestroy` | `beforeUnmount` |

## Publicação no GitHub Pages

Como o projeto é um único `index.html` na raiz do repositório, pode ser publicado diretamente:

1. No repositório `MiniProj1`, abrir **Settings → Pages**.
2. Em **Build and deployment**, escolher **Deploy from a branch**, ramo `main` e pasta `/ (root)`, e clicar em **Save**.
3. Após um ou dois minutos, o site fica disponível em `https://ernestobule-rgb.github.io/MiniProj1/`.

## Prototipagem

Os wireframes de todas as vistas, incluindo as janelas modais e a versão para telemóvel, estão disponíveis em três formatos:

- [Wireframes MiniProj1.pdf](<wireframes/Wireframes MiniProj1.pdf>): versão em PDF, pronta a consultar
- [Wireframes MiniProj1.drawio](<wireframes/Wireframes MiniProj1.drawio>): versão editável, que abre no [draw.io](https://app.diagrams.net)
- [wireframes.html](wireframes/wireframes.html): primeira versão dos wireframes, em HTML
