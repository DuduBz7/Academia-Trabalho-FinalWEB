# Trabalho Final de Web I — FitManager

Sistema web para gestão de uma academia, com páginas públicas, área do aluno e painel administrativo. Desenvolvido em HTML, CSS e JavaScript puro, com navegação entre páginas e um fluxo de login/cadastro que funciona com armazenamento local no navegador.

## Integrantes do grupo

- Luiz Eduardo Oliveira Mendes
- Luis Henrique Rodrigues Silva
- Maria Luiza Ramalho Almeida
- Iarley Oliveira de Jesus

### Introdução

**Objetivo:** desenvolver um sistema web de gestão para academias, contemplando tanto o site institucional (apresentação da academia, planos, professores e contato) quanto uma área autenticada com painéis distintos para alunos e administradores, colocando em prática os conceitos de HTML, CSS e JavaScript trabalhados na disciplina de Web I.

**Relevância:** academias lidam constantemente com cadastro de alunos, controle de planos, frequência e comunicação com a equipe de professores. Um sistema que centraliza essas informações em um só lugar, com acesso diferenciado por perfil, reduz retrabalho manual e melhora a experiência tanto de quem administra quanto de quem treina.

**Justificativa:** o tema "academia" foi escolhido por permitir explorar, em um domínio de fácil compreensão, diferentes tipos de página (institucionais, formulários e dashboards) e diferentes perfis de acesso (visitante, aluno e administrador), cobrindo boa parte dos desafios comuns do desenvolvimento front-end: layout responsivo, formulários, manipulação do DOM, navegação entre páginas HTML e persistência de dados no navegador.

### Desenvolvimento

#### Front-End

**Ferramentas, tecnologias e metodologias**

- **HTML5** semântico para a estrutura de todas as páginas
- **CSS3** puro, com variáveis (`:root`), Flexbox e CSS Grid para os layouts, e media queries para responsividade
- **JavaScript (Vanilla JS)**, sem frameworks ou bibliotecas externas, responsável por toda a interatividade e pelas regras de negócio
- **Web Storage API (`localStorage`)**, usada como banco de dados simulado no navegador, guardando os usuários cadastrados e a sessão do usuário atual
- Desenvolvimento incremental: primeiro as páginas institucionais estáticas, depois o fluxo de login/cadastro e, por fim, os painéis protegidos
- Reaproveitamento de código por meio da injeção de cabeçalho e rodapé via JavaScript (`js/app.js`) em todas as páginas, evitando duplicação de HTML

**Estrutura e funcionamento**

```
Trabalho-final-de-web-1/
├── index.html              # Página inicial (institucional)
├── css/
│   └── styles.css          # Estilos globais e responsivos
├── js/
│   └── app.js              # Autenticação, header/footer e painéis
└── pages/
    ├── sobre.html           # Página institucional "Sobre"
    ├── planos.html          # Planos e valores
    ├── professores.html     # Equipe de professores
    ├── contato.html         # Informações e formulário de contato
    ├── login.html           # Autenticação de usuários
    ├── cadastro.html        # Cadastro de novos alunos
    ├── painel-aluno.html    # Painel protegido do aluno
    └── painel-admin.html    # Painel protegido do administrador
```

A página inicial (`index.html`) apresenta a proposta da academia com uma seção de destaque, números institucionais e os diferenciais do sistema. As páginas em `pages/` cobrem o conteúdo institucional (Sobre, Planos, Professores, Contato) e a área autenticada (Login, Cadastro, Painel do Aluno e Painel do Administrador).

Funcionamento geral:

1. **Navegação comum:** todas as páginas carregam o mesmo `app.js`, que injeta dinamicamente o cabeçalho (`#site-header`) e o rodapé (`#site-footer`) e ajusta os links de acordo com a pasta atual (raiz ou `pages/`).
2. **Cadastro:** o formulário em `cadastro.html` cria um novo usuário (nome, e-mail, senha e plano) e o salva na lista armazenada na chave `fitmanager-users` do `localStorage`, impedindo e-mails duplicados.
3. **Login:** o formulário em `login.html` valida e-mail e senha contra os usuários salvos em `fitmanager-users`. Se as credenciais forem válidas, o usuário é redirecionado ao painel correspondente ao seu perfil (administrador ou aluno); caso contrário, uma mensagem de erro é exibida.
4. **Sessão:** ao autenticar, os dados do usuário logado são salvos na chave `fitmanager-current-user` do `localStorage`. O cabeçalho passa a exibir "Meu painel" e um botão "Sair" no lugar do link de login.
5. **Painéis protegidos:** `painel-aluno.html` e `painel-admin.html` usam um atributo `data-required-role` (`student` ou `admin`) em conjunto com JavaScript para verificar se existe um usuário logado e se o perfil corresponde ao exigido pela página. Sem login ou com perfil incompatível, o conteúdo é ocultado e uma mensagem de acesso é exibida no lugar.
6. **Usuários de demonstração:** na primeira execução, o sistema garante automaticamente a existência de um usuário administrador e um usuário aluno para teste (veja credenciais mais abaixo).
7. **Responsividade:** o layout usa CSS Grid para organizar cartões, tabelas e seções, com breakpoints em 900px e 600px que reorganizam os elementos em coluna única em telas menores.

### Conclusão

**Desafios enfrentados**

- Reaproveitar cabeçalho e rodapé em várias páginas sem um framework, sendo necessário injetá-los via JavaScript e ajustar caminhos relativos conforme a pasta do arquivo
- Simular autenticação e controle de acesso por perfil (aluno/administrador) usando apenas `localStorage`, sem um back-end real
- Manter a responsividade em páginas com muitos cartões e tabelas, como os painéis do aluno e do administrador, sem comprometer a leitura em telas menores

**Trabalhos futuros / continuação**

- Implementar CRUD completo de alunos, professores e treinos (hoje os dados exibidos nos painéis são ilustrativos/fixos)
- Adicionar gráficos ao dashboard administrativo (frequência, evolução de alunos, receita por plano, etc.)
- Implementar modo escuro/claro alternável
- Adicionar busca e filtros em tempo real nas listagens
- Conectar o formulário da página de contato a um serviço real de envio de mensagens
- Substituir o armazenamento em `localStorage` por uma API com banco de dados real

## Como executar

1. Clone ou baixe este repositório.
2. Acesse a pasta do projeto pelo terminal.
3. Inicie um servidor local, por exemplo:
   ```
   python3 -m http.server 8000
   ```
4. Abra o navegador em `http://127.0.0.1:8000/`

## Usuários de demonstração

| Perfil | E-mail | Senha |
|---|---|---|
| Administrador | admin@fitmanager.com | admin123 |
| Aluno | aluno@fitmanager.com | aluno123 
