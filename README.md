# Estudos Spring Data JPA — Bookstore

Projeto de estudos sobre **Spring Data JPA**, com foco no mapeamento de relacionamentos entre entidades: `@OneToOne`, `@OneToMany`, `@ManyToOne` e `@ManyToMany`.

## Sobre o projeto

Simula um pequeno sistema de livraria para explorar, na prática, como o Spring Data JPA (via Hibernate) traduz relacionamentos entre entidades Java em tabelas e chaves estrangeiras no banco de dados.

## Tecnologias

- Java
- Spring Boot
- Spring Data JPA
- Jakarta Persistence (JPA)
- Maven

## Entidades e relacionamentos

### `BookModel` (TB_BOOK)
Entidade central do projeto:
- **Publisher** → `@ManyToOne`: cada livro pertence a uma única editora.
- **Authors** → `@ManyToMany`: um livro pode ter vários autores, e um autor pode ter vários livros (tabela associativa `tb_book_author`).
- **Review** → `@OneToOne`: cada livro tem no máximo uma avaliação (lado inverso, `mappedBy`, com `cascade = ALL`).

### `PublisherModel` (TB_PUBLISHER)
- **Books** → `@OneToMany` (`mappedBy = "publisher"`): uma editora pode publicar vários livros. Lado inverso, carregamento `LAZY`.

### `AuthorModel` (TB_AUTHOR)
- **Books** → `@ManyToMany` (`mappedBy = "authors"`): lado inverso do relacionamento com `BookModel`, carregamento `LAZY`.

### `ReviewModel` (TB_REVIEW)
- **Book** → `@OneToOne`: lado dono do relacionamento, com chave estrangeira `book_id`.

## Resumo dos relacionamentos

| Relação | Tipo | Lado dono | Observação |
|---|---|---|---|
| Book ↔ Publisher | Many-to-One / One-to-Many | Book | Um Publisher tem vários Books |
| Book ↔ Author | Many-to-Many | Book | Tabela associativa `tb_book_author` |
| Book ↔ Review | One-to-One | Review | `cascade = ALL` no lado inverso (Book) |

## Objetivo do estudo

- Diferença entre lado dono e lado inverso (`mappedBy`) dos relacionamentos.
- Uso de `@JoinColumn` e `@JoinTable`.
- Estratégias de fetch (`LAZY` vs padrão).
- Cascade types.
- `JpaRepository` e query methods derivados (ex: `findBookModelByTitle`).

## Como rodar

```bash
./mvnw spring-boot:run
```
