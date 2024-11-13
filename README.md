

![Logo FIAP](https://github.com/Vitor-coder-eng/agricultural-database/blob/main/logo-fiap.png)

# agricultural-database
Repositório para o projeto de banco de dados sobre produção de trigo no Brasil com scripts SQL, consultas e documentação
# Projeto de Banco de Dados Agrícola

Este projeto visa criar um banco de dados para armazenar informações sobre a produção agrícola, incluindo dados de cultura, safra, estado e produção. 

## Índice

1. [Descrição do Projeto](#descrição-do-projeto)
2. [Modelagem de Dados](#modelagem-de-dados)
3. [Diagrama Entidade-Relacionamento (MER)](#diagrama-entidade-relacionamento-mer)
4. [Modelo Relacional](#modelo-relacional)
5. [Código SQL para Criação das Tabelas](#código-sql-para-criação-das-tabelas)
6. [Consultas SQL](#consultas-sql)
7. [Dicionário de Dados](#dicionário-de-dados)
8. [Documentação](#documentação)

---

### Descrição do Projeto

Este projeto foi desenvolvido para fornecer um banco de dados que auxilie no armazenamento e análise de dados agrícolas. Ele permite consultar a produção agrícola por estado, safra e cultura, fornecendo informações como produtividade, área plantada e volume de produção.

### Modelagem de Dados

Aqui está uma visão geral da modelagem de dados utilizada para criar o banco de dados agrícola.

#### Diagrama Entidade-Relacionamento (MER)
*Insira aqui uma imagem do diagrama Entidade-Relacionamento (MER)*

#### Modelo Relacional
*Insira aqui uma imagem do diagrama do modelo relacional ou uma descrição do modelo.*

### Código SQL para Criação das Tabelas

Abaixo está o código SQL usado para criar as tabelas do banco de dados:

```sql
-- Código SQL para criação das tabelas
CREATE TABLE Cultura (
    id_cultura INT PRIMARY KEY,
    nome VARCHAR(50) NOT NULL
);

CREATE TABLE Safra (
    id_safra INT PRIMARY KEY,
    ano INT NOT NULL
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
