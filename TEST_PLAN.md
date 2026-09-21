# PLANO DE TESTES E CASOS DE TESTE MANUAIS

**Sistema:** React + NestJS Movies DB
**Tipo de Teste:** Testes Funcionais Manuais
**Técnicas Aplicadas:**

* Particionamento de Equivalência
* Análise de Valor Limite
* Tabela de Decisão

---

# 1. INTRODUÇÃO

Este documento descreve o plano de testes e os casos de teste manuais aplicados ao sistema de gerenciamento de filmes desenvolvido com React (frontend) e NestJS (backend). O objetivo é validar o comportamento funcional do sistema sob diferentes condições de entrada, utilizando técnicas clássicas de teste de software.

---

# 2. OBJETIVO

Garantir que as funcionalidades principais do sistema:

* Funcionem conforme esperado
* Tratem entradas inválidas corretamente
* Respeitem regras de negócio

---

# 3. ESCOPO

## 3.1 Funcionalidades testadas

* Cadastro de usuário (Sign Up)
* Login
* Busca de filmes (integração com API externa)
* CRUD de filmes:

  * Adicionar
  * Editar
  * Remover
  * Listar

## 3.2 Fora de escopo

* Testes de performance
* Testes de segurança avançada
* Testes automatizados

---

# 4. AMBIENTE DE TESTE

* Navegador: Google Chrome
* Backend: NestJS
* Frontend: React
* API externa: TMDB (The Movie Database)
* Sistema operacional: Windows 11

---

# 5. ESTRATÉGIA DE TESTE

## 5.1 Particionamento de Equivalência

Divide entradas em classes:

* Válidas
* Inválidas

## 5.2 Valor Limite

Testa extremos:

* Mínimo permitido
* Máximo permitido

## 5.3 Tabela de Decisão

Valida regras de negócio com múltiplas condições

---

# 6. CASOS DE TESTE

---

# 6.1 CADASTRO DE USUÁRIO (SIGN UP)

## 6.1.1 Particionamento de Equivalência

| Classe   | Entrada                              | Resultado Esperado |
| -------- | ------------------------------------ | ------------------ |
| Válido   | Email válido + senha >= 6 caracteres | Cadastro realizado |
| Inválido | Email sem "@"                        | Erro de validação  |
| Inválido | Email vazio                          | Erro               |
| Inválido | Senha vazia                          | Erro               |
| Inválido | Senha < 6 caracteres                 | Erro               |

---

## 6.1.2 Valor Limite

| Campo | Limite | Entrada        | Resultado          |
| ----- | ------ | -------------- | ------------------ |
| Senha | Mínimo | 6 caracteres   | Aceito             |
| Senha | Abaixo | 5 caracteres   | Rejeitado          |
| Email | Mínimo | 1 caractere    | Rejeitado          |
| Email | Máximo | 255 caracteres | Aceito (se válido) |

---

## 6.1.3 Casos de Teste

### CT01 – Cadastro válido

* Pré-condição: Usuário não cadastrado
* Passos:

  1. Acessar tela de cadastro
  2. Inserir email válido
  3. Inserir senha >= 6 caracteres
  4. Clicar em "Sign Up"
* Resultado esperado:

  * Usuário cadastrado
  * Redirecionamento ou mensagem de sucesso

---

### CT02 – Email inválido

* Entrada: "usuario.com"
* Resultado esperado:

  * Mensagem de erro de validação

---

### CT03 – Senha abaixo do limite

* Entrada: "12345"
* Resultado esperado:

  * Sistema rejeita cadastro

---

---

# 6.2 LOGIN

## 6.2.1 Particionamento de Equivalência

| Classe   | Entrada                | Resultado |
| -------- | ---------------------- | --------- |
| Válido   | Email + senha corretos | Login OK  |
| Inválido | Senha incorreta        | Erro      |
| Inválido | Usuário inexistente    | Erro      |
| Inválido | Campos vazios          | Erro      |

---

## 6.2.2 Tabela de Decisão

| Email existe | Senha correta | Resultado       |
| ------------ | ------------- | --------------- |
| Sim          | Sim           | Login permitido |
| Sim          | Não           | Erro            |
| Não          | Sim           | Erro            |
| Não          | Não           | Erro            |

---

## 6.2.3 Casos de Teste

### CT04 – Login válido

* Entrada: credenciais corretas
* Resultado esperado:

  * Acesso ao sistema

---

### CT05 – Senha incorreta

* Resultado esperado:

  * Mensagem "credenciais inválidas"

---

### CT06 – Usuário inexistente

* Resultado esperado:

  * Mensagem de erro

---

---

# 6.3 BUSCA DE FILMES

## 6.3.1 Particionamento

| Classe   | Entrada              | Resultado           |
| -------- | -------------------- | ------------------- |
| Válido   | Nome de filme        | Lista exibida       |
| Inválido | Campo vazio          | Nenhum resultado    |
| Inválido | Caracteres especiais | Tratamento sem erro |

---

## 6.3.2 Valor Limite

| Caso   | Entrada             | Resultado        |
| ------ | ------------------- | ---------------- |
| Mínimo | 1 caractere         | Busca executada  |
| Máximo | string longa (100+) | Sistema responde |

---

## 6.3.3 Casos de Teste

### CT07 – Busca válida

* Entrada: "Batman"
* Resultado esperado:

  * Lista de filmes exibida

---

### CT08 – Busca vazia

* Resultado esperado:

  * Nenhum resultado ou bloqueio

---

---

# 6.4 CRUD DE FILMES

---

## 6.4.1 Adicionar Filme

### Particionamento

| Classe   | Entrada           | Resultado        |
| -------- | ----------------- | ---------------- |
| Válido   | Dados completos   | Filme adicionado |
| Inválido | Título vazio      | Erro             |
| Inválido | Dados incompletos | Erro             |

---

### Casos de Teste

### CT09 – Adicionar válido

* Resultado esperado:

  * Filme aparece na lista

---

### CT10 – Adicionar inválido

* Resultado esperado:

  * Sistema bloqueia ação

---

---

## 6.4.2 Editar Filme

### Tabela de Decisão

| Filme existe | Dados válidos | Resultado |
| ------------ | ------------- | --------- |
| Sim          | Sim           | Atualiza  |
| Sim          | Não           | Erro      |
| Não          | Sim           | Erro      |

---

### Casos

### CT11 – Editar válido

* Resultado esperado:

  * Dados atualizados

---

### CT12 – Editar inválido

* Resultado esperado:

  * Mensagem de erro

---

---

## 6.4.3 Remover Filme

### Casos

### CT13 – Remoção válida

* Passos:

  1. Selecionar filme
  2. Clicar em deletar
* Resultado esperado:

  * Filme removido

---

### CT14 – Remoção de item inexistente

* Resultado esperado:

  * Sistema não quebra / erro controlado

---

---

# 6.5 CASOS DE BORDA (VALOR LIMITE GERAL)

| Cenário                 | Resultado Esperado |
| ----------------------- | ------------------ |
| Lista vazia             | Interface estável  |
| Muitos filmes           | Sistema não trava  |
| Nome extremamente longo | Não quebra layout  |
| API fora do ar          | Tratamento de erro |

---

# 7. CRITÉRIOS DE ACEITAÇÃO

* 100% dos testes críticos aprovados
* Nenhum erro bloqueante
* Mensagens de erro claras
* Sistema não deve quebrar em entradas inválidas

---

# 8. RISCOS

* Dependência da API externa (TMDB)
* Falhas de validação no frontend/backend
* Dados inconsistentes

---

# 9. CONCLUSÃO

O plano de testes garante cobertura das principais funcionalidades do sistema, aplicando técnicas fundamentais de teste de software. A abordagem permite identificar falhas tanto em validações quanto em regras de negócio, assegurando maior confiabilidade do sistema.
=======
