

![Logo FIAP](https://github.com/Vitor-coder-eng/agricultural-database/blob/main/logo-fiap.png)

# Produção agrícola no Brasil


# Índice

1. [Descrição do Projeto](#descrição-do-projeto)
2. [Modelagem de Dados](#modelagem-de-dados)
3. [Diagrama Entidade-Relacionamento (MER)](#diagrama-entidade-relacionamento-mer)
4. [Modelo Lógico](#modelo-lógico)
5. [Código SQL para Criação das Tabelas](#código-sql-para-criação-das-tabelas)
6. [Consultas SQL](#consultas-sql)
7. [Dicionário de Dados](#dicionário-de-dados)
8. [Conclusão](#conclusão)

---

# Descrição do Projeto

Este projeto foi desenvolvido para fornecer um banco de dados que auxilie no armazenamento e análise de dados agrícolas. Usamos a base de dados da Série Histórica de Trigo no Brasil da CONAB, porém, ele pode ser facilmente modificado para outras culturas. Ele permite consultar a produção agrícola por estado, safra e cultura, fornecendo informações como produtividade, área plantada e volume de produção.

# Modelagem de Dados

# Diagrama Entidade-Relacionamento (MER)
![ Diagrama Entidade-Relacionamento](https://github.com/Vitor-coder-eng/agricultural-database/blob/main/Modelo%20Entidade-Relacionamento.png)

# Modelo Lógico
![Modelo Relacional](https://github.com/Vitor-coder-eng/agricultural-database/blob/main/Modelo%20L%C3%B3gico)

# Código SQL para Criação das Tabelas

```sql
CREATE TABLE Cultura (
    id_cultura INT PRIMARY KEY,
    nome VARCHAR(50) NOT NULL
);

CREATE TABLE Safra (
    id_safra INT PRIMARY KEY,
    ano INT NOT NULL
);

CREATE TABLE Regiao (
    id_regiao INT PRIMARY KEY,
    nome VARCHAR(50) NOT NULL
);

CREATE TABLE Estado (
    id_estado INT PRIMARY KEY,
    nome VARCHAR(50) NOT NULL,
    id_regiao INT,
    FOREIGN KEY (id_regiao) REFERENCES Regiao(id_regiao)
);

CREATE TABLE Producao (
    id_producao INT PRIMARY KEY,
    producao_mil_toneladas FLOAT,
    area_mil_ha FLOAT,
    produtividade_kg_ha FLOAT,
    id_cultura INT,
    id_estado INT,
    id_safra INT,
    FOREIGN KEY (id_cultura) REFERENCES Cultura(id_cultura),
    FOREIGN KEY (id_estado) REFERENCES Estado(id_estado),
    FOREIGN KEY (id_safra) REFERENCES Safra(id_safra)
);

```
# Consultas SQL

### Produção total de trigo por estado em uma safra:

```sql
SELECT e.nome AS estado, SUM(p.producao_mil_toneladas) AS producao_total
FROM Producao p
JOIN Estado e ON p.id_estado = e.id_estado
WHERE p.id_cultura = <ID_DA_CULTURA> AND p.id_safra = <ID_DA_SAFRA>
GROUP BY e.nome;
```

### Evolução da área plantada de trigo ao longo dos anos:

```sql
SELECT s.ano, SUM(p.area_mil_ha) AS area_total
FROM Producao p
JOIN Safra s ON p.id_safra = s.id_safra
WHERE p.id_cultura = <ID_DA_CULTURA>
GROUP BY s.ano
ORDER BY s.ano;
```

### Ranking dos estados com maior produtividade de trigo

```sql
SELECT e.nome AS estado, AVG(p.produtividade_kg_ha) AS produtividade_media
FROM Producao p
JOIN Estado e ON p.id_estado = e.id_estado
WHERE p.id_cultura = <ID_DA_CULTURA>
GROUP BY e.nome
ORDER BY produtividade_media DESC;
```

# Dicionário de Dados

### Tabela: Cultura

id_cultura (INT): Identificador único da cultura.

nome (VARCHAR): Nome da cultura (ex: Trigo, Soja).

### Tabela: Safra

id_safra (INT): Identificador único da safra.

ano (INT): Ano da safra.

### Tabela: Regiao

id_regiao (INT): Identificador único da região

nome (VARCHAR): Nome da região

### Tabela: Estado

id_estado (INT): Identificador único do estado.

nome (VARCHAR): Nome do estado.

id_regiao (INT): Chave estrangeira que referencia a tabela Regiao.

### Tabela: Producao

id_producao (INT): Identificador único da produção.

producao_mil_toneladas (FLOAT): Quantidade produzida em mil toneladas.

area_mil_ha (FLOAT): Área plantada em mil hectares.

produtividade_kg_ha (FLOAT): Produtividade em kg/ha.

id_cultura (INT): Chave estrangeira para a tabela Cultura.

id_estado (INT): Chave estrangeira para a tabela Estado.

id_safra (INT): Chave estrangeira para a tabela Safra.

# Conclusão

Este projeto de modelagem de banco de dados foi desenvolvido para fornecer uma estrutura organizada e acessível para o armazenamento e análise de dados relacionados à produção agrícola no Brasil. Ao consolidar informações sobre culturas, safras, regiões e estados, o banco de dados possibilita consultas eficientes e permite uma visão abrangente do setor agrícola nacional. As consultas SQL preparadas, como análise da produção por safra e ranking de produtividade por estado, exemplificam o potencial do banco para apoiar decisões estratégicas e aprimorar a gestão de produção agrícola.

Futuras melhorias podem incluir a automação da atualização dos dados e integração com fontes externas. Essa base de dados proporciona uma plataforma sólida e escalável, capaz de evoluir conforme as demandas de análise e gestão do setor agrícola.


