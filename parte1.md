
# Desafio Técnico: DBA - Parte 1

## Contexto do Desafio:
Você foi contratado como DBA em uma EdTech que utiliza um sistema SaaS com bancos de dados hospedados principalmente no AWS RDS (foco no MySQL). A empresa enfrenta problemas de performance em suas queries, dificuldades na observabilidade de métricas importantes dos bancos e precisa garantir que a arquitetura atual seja escalável e de fácil manutenção.

Sua missão é diagnosticar e otimizar um banco de dados MySQL, configurar monitoramento para observabilidade e garantir que o sistema seja resiliente e de fácil manutenção a longo prazo.

---

## Parte 1: Configuração de um Ambiente DBaaS (MySQL no AWS RDS)

### Tarefa:
1. **Configuração do Banco de Dados (AWS RDS)**:
   - Simule um ambiente real criando uma instância MySQL utilizando **AWS RDS** (ou use uma instância local caso não tenha acesso ao AWS RDS).
   - Crie um banco de dados chamado `edtech_db` e crie tabelas, conforme descrição abaixo (você pode alterar ou adicionar novas tabelas). Esse arquivo deve conter:
     - Pelo menos **500 mil registros** para simular um cenário com carga de dados significativa.
     - Várias queries comuns, incluindo seleções simples e complexas que envolvem **joins (pelo menos 5 queries, com 2,3,4 e 5 tabelas diferentes na consulta), subqueries (pelo menos 3 queries) e agregações (pelo menos 3 queries)**.

---

## Estrutura Relacional:

### Tabela 1: `students` (Estudantes)
| Coluna          | Tipo         | Comentário                          |
|-----------------|--------------|-------------------------------------|
| `student_id`    | INT (PK)      | Identificador único do estudante    |
| `first_name`    | VARCHAR(50)   | Nome do estudante                   |
| `last_name`     | VARCHAR(50)   | Sobrenome do estudante              |
| `birth_date`    | DATE          | Data de nascimento                  |
| `gender`        | VARCHAR(10)   | Gênero (M/F/Outro)                  |
| `email`         | VARCHAR(100)  | Email do estudante                  |
| `phone`         | VARCHAR(15)   | Telefone do estudante               |
| `address_id`    | INT (FK)      | Referência à tabela de endereços    |

---

### Tabela 2: `addresses` (Endereços)
| Coluna           | Tipo         | Comentário                          |
|------------------|--------------|-------------------------------------|
| `address_id`     | INT (PK)      | Identificador único do endereço     |
| `street`         | VARCHAR(100)  | Nome da rua                         |
| `city`           | VARCHAR(50)   | Cidade                              |
| `state`          | VARCHAR(50)   | Estado                              |
| `postal_code`    | VARCHAR(10)   | Código postal                       |
| `country`        | VARCHAR(50)   | País                                |

---

### Tabela 3: `courses` (Cursos)
| Coluna          | Tipo         | Comentário                          |
|-----------------|--------------|-------------------------------------|
| `course_id`     | INT (PK)      | Identificador único do curso        |
| `course_name`   | VARCHAR(100)  | Nome do curso                       |
| `description`   | TEXT          | Descrição do curso                  |
| `start_date`    | DATE          | Data de início do curso             |
| `end_date`      | DATE          | Data de término do curso            |

---

### Tabela 4: `subjects` (Disciplinas)
| Coluna          | Tipo         | Comentário                          |
|-----------------|--------------|-------------------------------------|
| `subject_id`    | INT (PK)      | Identificador único da disciplina   |
| `subject_name`  | VARCHAR(100)  | Nome da disciplina                  |
| `course_id`     | INT (FK)      | Referência ao curso                 |
| `teacher_id`    | INT (FK)      | Referência ao professor da disciplina|

---

### Tabela 5: `teachers` (Professores)
| Coluna          | Tipo         | Comentário                          |
|-----------------|--------------|-------------------------------------|
| `teacher_id`    | INT (PK)      | Identificador único do professor    |
| `first_name`    | VARCHAR(50)   | Nome do professor                   |
| `last_name`     | VARCHAR(50)   | Sobrenome do professor              |
| `email`         | VARCHAR(100)  | Email do professor                  |
| `phone`         | VARCHAR(15)   | Telefone do professor               |

---

### Tabela 6: `enrollments` (Matrículas)
| Coluna          | Tipo         | Comentário                          |
|-----------------|--------------|-------------------------------------|
| `enrollment_id` | INT (PK)      | Identificador único da matrícula    |
| `student_id`    | INT (FK)      | Referência ao estudante             |
| `course_id`     | INT (FK)      | Referência ao curso                 |
| `enrollment_date`| DATE         | Data da matrícula                   |

---

### Tabela 7: `grades` (Notas)
| Coluna          | Tipo         | Comentário                          |
|-----------------|--------------|-------------------------------------|
| `grade_id`      | INT (PK)      | Identificador único da nota         |
| `student_id`    | INT (FK)      | Referência ao estudante             |
| `subject_id`    | INT (FK)      | Referência à disciplina             |
| `grade`         | DECIMAL(5,2)  | Nota do estudante na disciplina     |
| `grade_date`    | DATE          | Data da avaliação                   |

---

### Tabela 8: `assignments` (Trabalhos)
| Coluna          | Tipo         | Comentário                          |
|-----------------|--------------|-------------------------------------|
| `assignment_id` | INT (PK)      | Identificador único do trabalho     |
| `subject_id`    | INT (FK)      | Referência à disciplina             |
| `assignment_name`| VARCHAR(100) | Nome do trabalho                    |
| `due_date`      | DATE          | Data de entrega do trabalho         |
| `max_grade`     | DECIMAL(5,2)  | Nota máxima do trabalho             |

---

### Tabela 9: `attendance` (Presença)
| Coluna          | Tipo         | Comentário                          |
|-----------------|--------------|-------------------------------------|
| `attendance_id` | INT (PK)      | Identificador único da presença     |
| `student_id`    | INT (FK)      | Referência ao estudante             |
| `subject_id`    | INT (FK)      | Referência à disciplina             |
| `attendance_date`| DATE         | Data da presença                    |
| `status`        | VARCHAR(10)   | Presente/Ausente                    |

---

### Tabela 10: `payments` (Pagamentos)
| Coluna          | Tipo         | Comentário                          |
|-----------------|--------------|-------------------------------------|
| `payment_id`    | INT (PK)      | Identificador único do pagamento    |
| `student_id`    | INT (FK)      | Referência ao estudante             |
| `amount`        | DECIMAL(10,2) | Valor do pagamento                  |
| `payment_date`  | DATE          | Data do pagamento                   |
| `payment_method`| VARCHAR(20)   | Método de pagamento (Cartão, Boleto, etc.) |

---

### Normalização (1FN, 2FN, 3FN):

Aponte as tabelas que contenham as normalizações nos 3 tipos abaixo:

- **1ª Forma Normal (1FN)**: Todas as tabelas estão estruturadas com colunas que possuem valores atômicos (sem grupos repetidos).
- **2ª Forma Normal (2FN)**: Não há dependências parciais, já que todas as tabelas possuem uma chave primária simples ou composta, e todas as colunas não-chave dependem integralmente da chave primária.
- **3ª Forma Normal (3FN)**: Nenhuma tabela contém dependências transitivas, ou seja, todas as colunas são dependentes diretamente da chave primária, sem dependência de outras colunas não-chave.

--- 

### Entregáveis:

- Queries para criação do banco de dados e suas tabelas
- Queries para carga de dados (fake data)
- Diagrama de Entidades e Relacionamentos (em png, jpg, gif, pdf, etc).