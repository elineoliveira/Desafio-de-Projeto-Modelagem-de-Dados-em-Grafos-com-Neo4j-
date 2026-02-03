# Desafio de Projeto: Modelagem de Dados em Grafos com Neo4j 

Este repositório contém a resolução do desafio de modelagem de um serviço de streaming utilizando o banco de dados orientado a grafos **Neo4j**. 

O objetivo foi criar um grafo de conhecimento que conectasse usuários, conteúdos, gêneros e profissionais do cinema.

## Modelo Conceitual (Draft)

Devido ao desenvolvimento do projeto em ambiente mobile, a modelagem lógica foi realizada inicialmente de forma manuscrita para garantir a correta estruturação das entidades e seus relacionamentos.

![Foto do meu desenho no caderno em anexo]

### Estrutura do Grafo:
* **Nós (Labels):** User, Movie, Series, Genre, Actor, Director.
* **Relacionamentos:** * `WATCHED`: Conecta usuários a filmes/séries, incluindo a propriedade `rating` (nota).
  * `ACTED_IN`: Conecta atores aos conteúdos.
  * `DIRECTED`: Conecta diretores aos filmes.
  * `IN_GENRE`: Categoriza filmes e séries por gênero.

---

##  Implementação Técnica (Cypher)

Abaixo, apresento o script em linguagem **Cypher** que traduz o modelo desenhado acima para o ambiente do Neo4j:

```cypher
// 1. Criando os Gêneros
CREATE (ficcao:Genre {name: 'Ficção Científica'})
CREATE (animacao:Genre {name: 'Animação'})

// 2. Criando Filmes e Séries
CREATE (matrix:Movie {title: 'Matrix', release: 1999})
CREATE (reileao:Movie {title: 'O Rei Leão', release: 1994})
CREATE (stranger:Series {title: 'Stranger Things', seasons: 4})

// 3. Criando Pessoas (Atores e Diretores)
CREATE (keanu:Actor {name: 'Keanu Reeves'})
CREATE (winona:Actor {name: 'Winona Ryder'})
CREATE (lana:Director {name: 'Lana Wachowski'})

// 4. Criando Usuários
CREATE (ana:User {name: 'Ana'})
CREATE (bruno:User {name: 'Bruno'})

// --- Estabelecendo Conexões (Relacionamentos) ---

// Relacionamentos de Gênero
CREATE (matrix)-[:IN_GENRE]->(ficcao)
CREATE (stranger)-[:IN_GENRE]->(ficcao)
CREATE (reileao)-[:IN_GENRE]->(animacao)

// Relacionamentos Profissionais
CREATE (keanu)-[:ACTED_IN]->(matrix)
CREATE (winona)-[:ACTED_IN]->(stranger)
CREATE (lana)-[:DIRECTED]->(matrix)

// Relacionamentos de Consumo (Com propriedade Rating/Nota)
CREATE (ana)-[:WATCHED {rating: 5}]->(matrix)
CREATE (bruno)-[:WATCHED {rating: 4}]->(stranger)
![1000048171](https://github.com/user-attachments/assets/769c4b72-3669-4724-bdce-73cee7b97821)
