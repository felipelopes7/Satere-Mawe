<<<<<<< HEAD
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
cat << 'EOF' > TEST_PLAN.md
# 📋 Plano de Testes Manuais (Entrega 1)
**Projeto:** Full-Stack de Gerenciamento de Filmes (NestJS + Next.js)  
**Período Letivo:** 2026/02  
**Disciplina:** Verificação, Validação e Testes de Software  
**Escola Superior de Tecnologia – Universidade do Estado do Amazonas (UEA)**

---

## 📌 1. Introdução e Escopo
Este documento detalha o planejamento e a especificação dos **Casos de Teste Manuais** para a aplicação de gerenciamento de filmes baseada em NestJS (Backend) e Next.js (Frontend). 

O escopo dos testes manuais abrange as principais funcionalidades críticas do sistema:
1. **Módulo de Autenticação e Autorização** (Controle de acesso por perfis e JWT).
2. **Módulo de Cadastro e Gerenciamento de Filmes** (Validação de campos e regras de negócio).
3. **Módulo de Avaliação e Regras de Exibição** (Comportamento condicional para usuários assinantes e administradores).

---

## 🛠️ 2. Técnicas de Teste Aplicadas
Para garantir a cobertura de cenários válidos e inválidos sem redundância, foram utilizadas as seguintes técnicas de caixa-preta:
* **Particionamento de Equivalência:** Divisão dos dados de entrada em classes onde o comportamento do sistema deve ser homogêneo.
* **Análise do Valor Limite (AVL):** Foco nas bordas e extremidades das classes de entrada (limites aceitos e rejeitados).
* **Tabela de Decisão:** Mapeamento de combinações complexas de regras de negócios e permissões de acesso.

---

## 📝 3. Especificação dos Casos de Teste Manuais

### CT01: Cadastro de Filme - Ano de Lançamento (Particionamento de Equivalência)
* **Objetivo:** Validar se o sistema aceita anos válidos e rejeita anos inválidos (futuros ou anteriores à invenção do cinema).
* **Pré-condições:** Estar logado no painel administrativo do Next.js.
* **Passos:**
  1. Acessar a tela de cadastro de filmes.
  2. Preencher os dados obrigatórios e inserir o valor de teste no campo *Ano de Lançamento*.
  3. Clicar em "Salvar".

| ID do Subcaso | Valor de Entrada (Ano) | Tipo de Classe | Resultado Esperado | Status |
| :--- | :---: | :---: | :--- | :---: |
| **CT01.1** | `2024` | Válida | O sistema aceita o dado e prossegue com o cadastro com sucesso. | `[ ]` |
| **CT01.2** | `2030` | Inválida (Futuro) | O sistema rejeita a entrada e exibe mensagem de erro de ano futuro. | `[ ]` |
| **CT01.3** | `1850` | Inválida (Antigo) | O sistema rejeita a entrada e exibe mensagem de erro por data inválida. | `[ ]` |

---

### CT02: Cadastro de Filme - Nota/Avaliação do Filme (Análise do Valor Limite)
* **Objetivo:** Testar os limites de pontuação aceitos pelo sistema (escala de 0 a 5 estrelas).
* **Pré-condições:** Estar logado no painel administrativo.
* **Passos:** Inserir os valores de contorno no campo de avaliação de um filme.

| ID do Subcaso | Valor de Entrada | Limite / Adjacência | Resultado Esperado | Status |
| :--- | :---: | :--- | :--- | :---: |
| **CT02.1** | `-1` | Abaixo do Limite Inferior | Rejeição da nota (mensagem de erro). | `[ ]` |
| **CT02.2** | `0` | No Limite Inferior Exato | Aceitação da nota mínima (válido). | `[ ]` |
| **CT02.3** | `1` | Logo Acima do Limite Inferior | Aceitação da nota (válido). | `[ ]` |
| **CT02.4** | `4` | Logo Abaixo do Limite Superior | Aceitação da nota (válido). | `[ ]` |
| **CT02.5** | `5` | No Limite Superior Exato | Aceitação da nota máxima (válido). | `[ ]` |
| **CT02.6** | `6` | Acima do Limite Superior | Rejeição da nota (mensagem de erro). | `[ ]` |

---

### CT03: Permissões e Regras de Acesso (Tabela de Decisão)
* **Objetivo:** Validar as ações permitidas com base no perfil do usuário, status do filme e tipo de assinatura.
* **Pré-condições:** Possuir credenciais de Administrador e de Usuário Comum (com e sem assinatura Premium).

#### Matriz de Decisão:
| Condições / Regras | Regra 1 | Regra 2 | Regra 3 | Regra 4 | Regra 5 |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **É Administrador?** | Sim | Não | Não | Não | Não |
| **Filme está Ativo no Catálogo?** | - | Sim | Sim | Não | Não |
| **Tem Assinatura Premium?** | - | Sim | Não | Sim | Não |
| **Ações / Resultados Esperados** | | | | | |
| **Permitir Editar/Excluir Filme** | **X** | - | - | - | - |
| **Permitir Assistir ao Filme** | **X** | **X** | **X** *(Com anúncios)* | - | - |
| **Exibir Erro de Conteúdo Indisponível** | - | - | - | **X** | **X** |

* **Passos de Execução para validação (Exemplo Regra 3):**
  1. Logar com um usuário comum sem assinatura Premium.
  2. Acessar um filme com status ativo no catálogo.
  3. Tentar reproduzir o conteúdo.
  * *Resultado Esperado:* O sistema reproduz o filme, mas aplica as restrições do plano gratuito (exibindo anúncios).
EOF
>>>>>>> baf2a42 (ReadMe)
