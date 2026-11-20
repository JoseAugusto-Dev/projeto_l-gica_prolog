Sistema de Recomendação de Filmes em Prolog
Projeto avaliativo da disciplina Lógica para Ciências da Computação, desenvolvido em Prolog, que representa informações de filmes lançados entre 2000 e 2025 e responde a consultas lógicas para classificação, filtragem e recomendação.
Informações do Projeto
Disciplina: Lógica para Ciências da Computação
Linguagem: Prolog (codificação UTF-8)
Autor(es): João Ricardo / José Augusto
Estrutura do Repositório
`sistema de sugestão de filmes.pl`: base de conhecimento, predicados auxiliares, regras lógicas, predicados de consulta e exemplos comentados.
`README.md`: documentação do sistema e exemplos de uso.
Visão Geral do Código (`sistema de sugestão de filmes.pl`)
O código está organizado em cinco partes:
Base de Conhecimento (`filme/12`): fatos de filmes de 2000 a 2025 contendo título, ano, nota do público, nota da crítica, quantidade de Oscars, duração em minutos, gênero, diretor, país, data de lançamento, destaque (`EmAlta`) e bilheteria mundial em milhões de USD.
Predicados Auxiliares: extraem campos específicos de `filme/12` (`ano/2`, `nota_publico/2`, `nota_critica/2`, `oscars/2`, `duracao/2`, `genero/2`, `diretor/2`, `pais/2`, `em_alta/1`, `bilheteria/2`) para tornar as regras mais concisas e legíveis.
Regras Lógicas:
`nota_media/2`: calcula a média arredondada entre a nota do público e a da crítica.
`bem_avaliado/1`: verifica se a nota média é maior ou igual a `8.0`.
`premiado/1`: verifica se o filme ganhou pelo menos 1 Oscar.
`blockbuster/1`: verifica se a bilheteria mundial é de pelo menos 500 milhões de dólares.
`nacional/1`: identifica filmes produzidos no `'Brasil'`.
`filme_longo/1`: identifica filmes com duração igual ou superior a 150 minutos.
`recomendar/2`: recomenda filmes de um determinado gênero que sejam bem avaliados.
Predicados de Consulta: agrupam resultados em listas utilizando `setof/3` (`filmes_do_genero/2`, `filmes_do_diretor/2`, `filmes_do_ano/2`, `filmes_em_alta/1`).
Exemplos de Consultas: consultas comentadas ao final do arquivo com seus respectivos resultados.
Como Executar
Instale o SWI-Prolog na sua máquina.
Abra o terminal na pasta do projeto e inicie o interpretador carregando o arquivo:
```bash
   swipl "sistema de sugestão de filmes.pl"
   ```
Exemplos de Consultas e Resultados :
    Média entre público e crítica:

    ?- nota_media('Cidade de Deus', M).
    M = 8.25.

    Verificar se um filme é bem avaliado:
    ?- bem_avaliado('Parasita').
    true.

    Filmes brasileiros premiados com Oscar:
    ?- nacional(T), premiado(T).
    T = 'Ainda Estou Aqui'.

    Recomendar filmes de um gênero:
    ?- recomendar(romance, T).
    T = 'Brilho Eterno de uma Mente sem Lembrancas' ;
    T = 'Orgulho e Preconceito' ;
    T = 'Ela'.

    Listar filmes por diretor:
    ?- filmes_do_diretor('Christopher Nolan', Lista).
    Lista = ['A Origem', 'Batman Begins', 'Batman: O Cavaleiro das Trevas',
         'Dunkirk', 'Interestelar', 'O Cavaleiro das Trevas Ressurge',
         'O Grande Truque', 'Oppenheimer', 'Tenet'].

    Listar filmes por ano:
    ?- filmes_do_ano(2019, Lista).
    Lista = ['A Vida Invisivel', 'Bacurau', 'Coringa',
         'Era Uma Vez em... Hollywood', 'Midsommar: O Mal Nao Espera o Verao',
         'Nos', 'Parasita', 'Vingadores: Ultimato'].

    Consulta composta (blockbuster e filme longo):
    ?- blockbuster('Avatar'), filme_longo('Avatar').
    true.
