# Atividade I — Integração do Back-end com Banco de Dados

## 1. Objetivo

Dando continuidade à **Atividade III do 2º trimestre**, refatorar o `db.js` da atividade anterior, substituindo o armazenamento em memória por um **banco de dados real**.

Utilize a arquitetura:

```text
Router → Controller → Service → Repository → Banco de Dados
```

## 2. Banco de Dados

Escolha uma opção:

### MySQL

```bash
npm install mysql2
```

### PostgreSQL

Utilize o [Render](https://render.com/?utm_source=chatgpt.com).

```bash
npm install pg
```

> **Atenção:** devido ao Proxy da escola, o PostgreSQL/Render deve ser instalado e utilizado fora do ambiente da escola.

## 3. Pesquisa — Arquitetura

Antes de iniciar a implementação, **pesquise e compreenda os conceitos** da arquitetura utilizada no projeto:

```text
Router → Controller → Service → Repository → Banco de Dados
```

Pesquise e responda:

1. O que são **Routes (Rotas)**?
2. O que são **Controllers**?
3. O que são **Services**?
4. O que são **Repositories**?
5. **Compreenda o fluxo entre as camadas da arquitetura.**

## 4. Banco

Crie as tabelas:

### `perfil`

`id`, `nome`, `email`, `descricao`

### `cursos`

`id`, `fk_perfil`, `nome`, `horas`

### `certificados`

`id`, `fk_perfil`, `titulo`, `ano`

Relacionamentos:

```text
perfil 1:N cursos
perfil 1:N certificados
```

`fk_perfil` deve ser uma **chave estrangeira** para `perfil.id`.

O banco deve possuir **dados iniciais**.

## 5. MER

Crie o **Modelo Entidade-Relacionamento (MER)** correspondente ao banco.

Salve no projeto:

```text
docs/mer.png
```

## 6. Estrutura do Projeto

A estrutura deve seguir:

```text
/
├── src/
│   ├── app.js
│   │
│   ├── database/
│   │   ├── conexao.js
│   │   └── banco.sql
│   │
│   ├── routes/
│   │   └── portfolio.routes.js
│   │
│   ├── controllers/
│   │   └── portfolio.controller.js
│   │
│   ├── services/
│   │   ├── perfil.service.js
│   │   ├── curso.service.js
│   │   └── certificado.service.js
│   │
│   ├── repositories/
│   │   ├── perfil.repository.js
│   │   ├── curso.repository.js
│   │   └── certificado.repository.js
│   │
│   └── views/
│       └── portfolio.ejs
│
├── docs/
│   └── mer.png
│
├── .env
├── .gitignore
├── package.json
└── README.md
```

O `.env` **não deve ser enviado para o GitHub**.

## 7. Portfolio

A rota principal será:

```text
GET /
```

A página deve apresentar:

* Perfil;
* Cursos;
* Certificados.

**Portfolio não é uma entidade do banco.**

Não crie `portfolio.service.js`.

O Controller deve utilizar os Services necessários:

```text
PortfolioController
├── PerfilService
├── CursoService
└── CertificadoService
```

Cada Service utiliza seu respectivo Repository:

```text
PerfilService → PerfilRepository
CursoService → CursoRepository
CertificadoService → CertificadoRepository
```

## 8. Repository

Os Repositories são responsáveis pelo acesso ao banco.

**Todo SQL deve ficar nos Repositories.**

Quando necessário, utilize `JOIN` nas consultas SQL.

## 9. `banco.sql`

O arquivo:

```text
src/database/banco.sql
```

deve conter:

* criação das tabelas;
* chaves primárias;
* chaves estrangeiras;
* dados iniciais.

Não utilize mais o `db.js`.

## 10. Conexão

Crie:

```text
src/database/conexao.js
```

Utilize o arquivo `.env` para armazenar as configurações de conexão com o banco.

**Não envie o `.env` para o GitHub.**

## 11. GitHub

O projeto deve estar hospedado no GitHub.

O repositório deve conter:

```text
src/
docs/
.gitignore
package.json
README.md
```

O `.env` deve existir localmente, mas **não deve ser enviado ao GitHub**.

O `README.md` deve informar:

* banco utilizado;
* instalação;
* configuração;
* execução;
* estrutura do projeto.

## 12. Desafio Plus — Firebase

Implemente uma versão utilizando Firebase.

Mantenha a arquitetura:

```text
Router → Controller → Service → Repository → Firebase
```

## 13. Horários

| **Hor**   | **Seg**       | **Ter**       | **Qua** | **Qui**      | **Sex**      |
| --------- | ------------- | ------------- | ------- | ------------ | ------------ |
| **07:20** | -             | -             | -       | -            | -            |
| **08:10** | 3ºDS-C/CDADOS | COORD         | COORD   | 3ºDS-B/PMOBI | -            |
| **09:00** | 3ºDS-C/CDADOS | COORD         | COORD   | 3ºDS-B/PMOBI | COORD        |
| **10:05** | COORD         | COORD         | COORD   | COORD        | COORD        |
| **10:55** | COORD         | 3ºDS-B/CDADOS | COORD   | COORD        | 3ºDS-C/PMOBI |
| **11:45** | COORD         | 3ºDS-B/CDADOS | -       | COORD        | 3ºDS-C/PMOBI |

> *“A mente que se abre a uma nova ideia jamais volta ao seu tamanho original.”* — **Albert Einstein**
