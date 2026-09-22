# PLANO DE TESTES E CASOS DE TESTE MANUAIS

**Sistema:** React + NestJS Movies DB  
**Tipo de teste:** Testes funcionais manuais  
**Técnicas utilizadas:**
* Particionamento de Equivalência
* Análise de Valor Limite
* Tabela de Decisão
* Transição de Estados

**Ambiente previsto:**
* **Sistema operacional:** Windows 11
* **Navegador:** Google Chrome
* **Frontend:** React
* **Backend:** NestJS
* **Banco de dados:** PostgreSQL
* **API externa:** TMDB (The Movie Database)

---

## 1. Introdução
Este documento apresenta o plano de testes funcionais manuais para o sistema React + NestJS Movies DB, uma aplicação de gerenciamento de filmes composta por uma interface frontend desenvolvida em React e uma API backend desenvolvida em NestJS.

Os testes têm como finalidade verificar se as principais funcionalidades do sistema estão funcionando de acordo com os requisitos definidos, além de avaliar o comportamento da aplicação diante de entradas inválidas, valores limites e diferentes combinações de condições.

Serão utilizadas técnicas clássicas de teste de software para aumentar a cobertura dos cenários e identificar possíveis falhas de validação, regras de negócio, integração e comportamento da interface.

## 2. Objetivos
Os principais objetivos dos testes são:
* Verificar o funcionamento das funcionalidades principais do sistema.
* Validar o cadastro de usuários.
* Validar o processo de autenticação.
* Verificar a busca de filmes utilizando a API externa TMDB.
* Validar as operações de criação, consulta, edição e remoção de filmes.
* Verificar o tratamento de entradas inválidas.
* Verificar o comportamento do sistema em valores limites.
* Validar regras de negócio que dependem de múltiplas condições.
* Verificar as mudanças de estado durante os fluxos de autenticação e gerenciamento de filmes.
* Identificar e registrar defeitos encontrados durante a execução.

## 3. Escopo

### 3.1 Funcionalidades dentro do escopo
Serão testadas as seguintes funcionalidades:

**Cadastro de usuário**
* Cadastro com dados válidos.
* Validação de e-mail.
* Validação de senha.
* Campos obrigatórios.
* Tentativa de cadastro com usuário já existente.

**Login**
* Login com credenciais válidas.
* Login com senha incorreta.
* Login com usuário inexistente.
* Login com campos vazios.
* Alteração do estado do usuário após autenticação.

**Busca de filmes**
* Busca por nome de filme.
* Busca com campo vazio.
* Busca com caracteres especiais.
* Busca com termos inexistentes.
* Tratamento de resultados.

**Gerenciamento de filmes**
* Listagem de filmes.
* Adição de filmes.
* Edição de filmes.
* Remoção de filmes.
* Validação dos dados do filme.
* Comportamento quando o filme não existe.

**Autenticação e autorização**
* Acesso de usuário não autenticado.
* Acesso após login.
* Persistência da sessão/token.
* Logout.

### 3.2 Fora do escopo
Não serão realizados:
* Testes de performance.
* Testes de carga ou estresse.
* Testes de segurança avançada.
* Testes automatizados.
* Testes de infraestrutura ou deploy em produção.
* Avaliação aprofundada da disponibilidade da API TMDB.

## 4. Itens a serem testados

| ID | Item |
| :--- | :--- |
| **IT01** | Cadastro de usuário |
| **IT02** | Login |
| **IT03** | Autenticação |
| **IT04** | Busca de filmes |
| **IT05** | Listagem de filmes |
| **IT06** | Adição de filmes |
| **IT07** | Edição de filmes |
| **IT08** | Remoção de filmes |
| **IT09** | Validação de dados |
| **IT10** | Tratamento de erros |

## 5. Técnicas de teste utilizadas

### 5.1 Particionamento de Equivalência
As entradas serão divididas em classes equivalentes, considerando que valores pertencentes à mesma classe devem produzir comportamentos semelhantes.

**Exemplos:**
* **Para o campo de e-mail:**
  * *Classe válida:* e-mail contendo formato válido.
  * *Classe inválida:* e-mail sem @.
  * *Classe inválida:* campo vazio.
* **Para a senha:**
  * *Classe válida:* senha com quantidade mínima de caracteres.
  * *Classe inválida:* senha abaixo do tamanho mínimo.
  * *Classe inválida:* campo vazio.

Essa técnica permite reduzir a quantidade de testes necessários sem deixar de representar diferentes tipos de entrada.

### 5.2 Análise de Valor Limite
Serão testados valores próximos aos limites definidos pelas regras do sistema. Por exemplo, considerando uma senha mínima de 6 caracteres:

| Situação | Entrada | Resultado esperado |
| :--- | :--- | :--- |
| Abaixo do limite | 5 caracteres | Rejeitada |
| No limite | 6 caracteres | Aceita |
| Acima do limite | 7 caracteres | Aceita |

Também serão avaliados valores extremos em campos de texto, como nomes e títulos de filmes.

### 5.3 Tabela de Decisão
A tabela de decisão será utilizada quando o resultado de uma funcionalidade depender de mais de uma condição.

**Exemplo: Login**

| Usuário existe | Senha correta | Resultado |
| :---: | :---: | :--- |
| Sim | Sim | Login permitido |
| Sim | Não | Login rejeitado |
| Não | Sim | Login rejeitado |
| Não | Não | Login rejeitado |

Essa técnica permite verificar combinações de condições e garantir que cada regra de negócio seja contemplada.

### 5.4 Transição de Estados
A técnica de transição de estados será utilizada para funcionalidades cujo comportamento depende do estado atual do sistema ou do usuário.

**Fluxo de autenticação**
```text
┌─────────────────────┐
│ Usuário não         │
│ autenticado         │
└──────────┬──────────┘
           │
           │ Login válido
           ▼
┌─────────────────────┐
│ Usuário             │
│ autenticado         │
└──────────┬──────────┘
           │
           │ Logout
           ▼
┌─────────────────────┐
│ Usuário não         │
│ autenticado         │
└─────────────────────┘
```
Serão verificadas também transições inválidas, como tentar acessar funcionalidades protegidas sem estar autenticado.

## 6. Critérios de entrada
A execução dos testes será iniciada quando:
1. O sistema estiver instalado e disponível para execução.
2. Frontend e backend estiverem funcionando.
3. O banco de dados estiver configurado.
4. O navegador Google Chrome estiver disponível.
5. A aplicação puder ser acessada pelo navegador.
6. As funcionalidades previstas para teste estiverem implementadas.
7. Existirem dados iniciais suficientes para executar os testes necessários.
8. A API TMDB estiver disponível para os testes de integração.

## 7. Critérios de saída
A execução dos testes será considerada concluída quando:
1. Todos os casos de teste planejados forem executados.
2. Todos os casos de teste críticos tiverem resultado registrado.
3. Os defeitos encontrados forem documentados.
4. Pelo menos um defeito real for registrado em formato de bug report.
5. Os resultados de execução forem consolidados.
6. Os casos bloqueados tiverem sua causa registrada.
7. Os principais requisitos tiverem cobertura através da matriz de rastreabilidade.

## 8. Riscos

| ID | Risco | Impacto | Mitigação |
| :--- | :--- | :---: | :--- |
| **R01** | API TMDB indisponível | Alto | Registrar o teste como bloqueado quando a indisponibilidade impedir sua execução |
| **R02** | Falha na comunicação frontend/backend | Alto | Verificar backend antes da execução dos testes funcionais |
| **R03** | Banco de dados indisponível | Alto | Validar conexão antes do início dos testes |
| **R04** | Dados de teste inconsistentes | Médio | Criar dados específicos para execução dos casos |
| **R05** | Falhas de validação | Médio | Utilizar entradas válidas e inválidas |
| **R06** | Token de autenticação inválido ou expirado | Médio | Executar testes de transição de estados |
| **R07** | Alterações na API externa | Médio | Registrar versão/data da execução |
| **R08** | Diferenças de comportamento entre ambientes | Médio | Executar os testes no ambiente definido neste documento |

---

## 9. Casos de teste

### 9.1 Cadastro de usuário

#### CT01 - Cadastro com dados válidos
* **Técnica:** Particionamento de Equivalência
* **Requisito:** RF01 - O sistema deve permitir o cadastro de usuários.
* **Pré-condição:** Usuário não cadastrado. Tela de cadastro disponível.
* **Passos:**
  1. Acessar a tela de cadastro.
  2. Informar um e-mail válido.
  3. Informar uma senha válida.
  4. Clicar em "Sign Up".
* **Resultado esperado:** O sistema deve cadastrar o usuário e apresentar uma confirmação de sucesso ou redirecionar para a área correspondente.

#### CT02 - Cadastro com e-mail inválido
* **Técnica:** Particionamento de Equivalência
* **Requisito:** RF01
* **Pré-condição:** Tela de cadastro disponível.
* **Passos:**
  1. Acessar a tela de cadastro.
  2. Informar `usuario.com` no campo de e-mail.
  3. Informar uma senha válida.
  4. Enviar o formulário.
* **Resultado esperado:** O sistema deve rejeitar o cadastro e apresentar uma mensagem de validação indicando que o e-mail é inválido.

#### CT03 - Cadastro com senha abaixo do limite
* **Técnica:** Valor Limite
* **Requisito:** RF01
* **Pré-condição:** Tela de cadastro disponível.
* **Passos:**
  1. Informar um e-mail válido.
  2. Informar uma senha com 5 caracteres.
  3. Enviar o formulário.
* **Resultado esperado:** O sistema deve rejeitar o cadastro.

#### CT04 - Cadastro com senha exatamente no limite
* **Técnica:** Valor Limite
* **Requisito:** RF01
* **Pré-condição:** Tela de cadastro disponível.
* **Passos:**
  1. Informar um e-mail válido.
  2. Informar uma senha com exatamente 6 caracteres.
  3. Enviar o formulário.
* **Resultado esperado:** O sistema deve aceitar a senha, caso 6 caracteres seja o limite mínimo definido pela regra de negócio.

#### CT05 - Cadastro com campos obrigatórios vazios
* **Técnica:** Particionamento de Equivalência
* **Requisito:** RF01
* **Pré-condição:** Tela de cadastro disponível.
* **Passos:**
  1. Acessar a tela de cadastro.
  2. Deixar o e-mail vazio.
  3. Deixar a senha vazia.
  4. Enviar o formulário.
* **Resultado esperado:** O sistema deve impedir o cadastro e informar que os campos obrigatórios precisam ser preenchidos.

---

### 9.2 Login

#### CT06 - Login com credenciais válidas
* **Técnica:** Tabela de Decisão
* **Requisito:** RF02 - O sistema deve permitir autenticação de usuários cadastrados.
* **Pré-condição:** Usuário cadastrado. E-mail e senha conhecidos.
* **Passos:**
  1. Acessar a tela de login.
  2. Informar o e-mail cadastrado.
  3. Informar a senha correta.
  4. Clicar em "Login".
* **Resultado esperado:** O sistema deve autenticar o usuário e permitir acesso às funcionalidades protegidas.

#### CT07 - Login com senha incorreta
* **Técnica:** Tabela de Decisão
* **Requisito:** RF02
* **Pré-condição:** Usuário cadastrado.
* **Passos:**
  1. Informar um e-mail cadastrado.
  2. Informar uma senha incorreta.
  3. Clicar em "Login".
* **Resultado esperado:** O sistema deve rejeitar a autenticação e apresentar uma mensagem de erro.

#### CT08 - Login com usuário inexistente
* **Técnica:** Tabela de Decisão
* **Requisito:** RF02
* **Pré-condição:** O e-mail utilizado não pertence a um usuário cadastrado.
* **Passos:**
  1. Informar um e-mail inexistente.
  2. Informar uma senha.
  3. Clicar em "Login".
* **Resultado esperado:** O sistema deve rejeitar a autenticação e apresentar uma mensagem de erro.

#### CT09 - Login com campos vazios
* **Técnica:** Particionamento de Equivalência
* **Requisito:** RF02
* **Pré-condição:** Tela de login disponível.
* **Passos:**
  1. Deixar o e-mail vazio.
  2. Deixar a senha vazia.
  3. Clicar em "Login".
* **Resultado esperado:** O sistema deve impedir a tentativa de autenticação ou apresentar mensagens de validação.

---

### 9.3 Busca de filmes

#### CT10 - Busca por filme existente
* **Técnica:** Particionamento de Equivalência
* **Requisito:** RF03 - O sistema deve permitir a busca de filmes.
* **Pré-condição:** Sistema disponível. API TMDB disponível.
* **Passos:**
  1. Acessar a funcionalidade de busca.
  2. Informar `Batman`.
  3. Executar a busca.
* **Resultado esperado:** O sistema deve apresentar filmes relacionados ao termo pesquisado.

#### CT11 - Busca com campo vazio
* **Técnica:** Particionamento de Equivalência
* **Requisito:** RF03
* **Pré-condição:** Funcionalidade de busca disponível.
* **Passos:**
  1. Deixar o campo de busca vazio.
  2. Executar a busca.
* **Resultado esperado:** O sistema deve impedir a busca ou apresentar nenhum resultado, sem quebrar a interface.

#### CT12 - Busca com termo inexistente
* **Técnica:** Particionamento de Equivalência
* **Requisito:** RF03
* **Pré-condição:** API TMDB disponível.
* **Passos:**
  1. Informar um termo que provavelmente não corresponda a nenhum filme.
  2. Executar a busca.
* **Resultado esperado:** O sistema deve apresentar uma lista vazia ou uma mensagem informando que nenhum filme foi encontrado.

#### CT13 - Busca com termo muito longo
* **Técnica:** Valor Limite
* **Requisito:** RF03
* **Pré-condição:** Funcionalidade de busca disponível.
* **Passos:**
  1. Inserir uma sequência de caracteres com mais de 100 caracteres.
  2. Executar a busca.
* **Resultado esperado:** O sistema deve tratar a entrada sem quebrar a interface ou apresentar erro não tratado.

---

### 9.4 Gerenciamento de filmes

#### CT14 - Adicionar filme com dados válidos
* **Técnica:** Particionamento de Equivalência
* **Requisito:** RF04 - O sistema deve permitir adicionar filmes.
* **Pré-condição:** Usuário autenticado. Dados válidos do filme disponíveis.
* **Passos:**
  1. Acessar a funcionalidade de adicionar filme.
  2. Preencher os campos obrigatórios.
  3. Confirmar o cadastro.
* **Resultado esperado:** O filme deve ser criado e aparecer na lista de filmes do usuário.

#### CT15 - Adicionar filme com título vazio
* **Técnica:** Particionamento de Equivalência
* **Requisito:** RF04
* **Pré-condição:** Usuário autenticado. Tela de cadastro de filme disponível.
* **Passos:**
  1. Deixar o campo título vazio.
  2. Preencher os demais campos obrigatórios.
  3. Tentar salvar o filme.
* **Resultado esperado:** O sistema deve rejeitar o cadastro e informar que o título é obrigatório.

#### CT16 - Editar filme existente com dados válidos
* **Técnica:** Tabela de Decisão
* **Requisito:** RF05 - O sistema deve permitir editar filmes.
* **Pré-condição:** Usuário autenticado. Filme existente.
* **Passos:**
  1. Selecionar um filme existente.
  2. Alterar uma informação válida.
  3. Salvar as alterações.
* **Resultado esperado:** As informações do filme devem ser atualizadas e permanecer alteradas após a atualização da lista.

#### CT17 - Editar filme com dados inválidos
* **Técnica:** Tabela de Decisão
* **Requisito:** RF05
* **Pré-condição:** Usuário autenticado. Filme existente.
* **Passos:**
  1. Selecionar um filme.
  2. Remover uma informação obrigatória.
  3. Tentar salvar as alterações.
* **Resultado esperado:** O sistema deve rejeitar a alteração e informar o problema ao usuário.

#### CT18 - Remover filme existente
* **Técnica:** Transição de Estados
* **Requisito:** RF06 - O sistema deve permitir remover filmes.
* **Pré-condição:** Usuário autenticado. Filme existente.  
  * *Estado inicial:* Filme existente
* **Passos:**
  1. Selecionar um filme.
  2. Clicar na opção de remoção.
  3. Confirmar a operação, caso exista confirmação.
* **Resultado esperado:** O filme deve deixar de aparecer na lista.  
  * *Estado final:* Filme removido

#### CT19 - Acessar funcionalidade protegida sem autenticação
* **Técnica:** Transição de Estados
* **Requisito:** RF07 - O sistema deve proteger funcionalidades que exigem autenticação.
* **Pré-condição:** Usuário não autenticado.  
  * *Estado inicial:* Não autenticado
* **Passos:**
  1. Tentar acessar diretamente uma funcionalidade protegida.
  2. Observar o comportamento do sistema.
* **Resultado esperado:** O sistema deve impedir o acesso ou redirecionar o usuário para a tela de login.

#### CT20 - Logout
* **Técnica:** Transição de Estados
* **Requisito:** RF07
* **Pré-condição:** Usuário autenticado.  
  * *Estado inicial:* Autenticado
* **Passos:**
  1. Acessar a opção de logout.
  2. Confirmar a saída, caso solicitado.
  3. Tentar acessar novamente uma funcionalidade protegida.
* **Resultado esperado:** O usuário deve deixar de estar autenticado e não deve conseguir acessar funcionalidades protegidas sem realizar novo login.  
  * *Estado final:* Não autenticado

---

## 10. Resumo dos casos de teste

| ID | Funcionalidade | Técnica |
| :--- | :--- | :--- |
| **CT01** | Cadastro válido | Particionamento |
| **CT02** | E-mail inválido | Particionamento |
| **CT03** | Senha abaixo do limite | Valor Limite |
| **CT04** | Senha no limite | Valor Limite |
| **CT05** | Campos vazios | Particionamento |
| **CT06** | Login válido | Tabela de Decisão |
| **CT07** | Senha incorreta | Tabela de Decisão |
| **CT08** | Usuário inexistente | Tabela de Decisão |
| **CT09** | Login vazio | Particionamento |
| **CT10** | Busca válida | Particionamento |
| **CT11** | Busca vazia | Particionamento |
| **CT12** | Filme inexistente | Particionamento |
| **CT13** | Busca longa | Valor Limite |
| **CT14** | Adicionar filme | Particionamento |
| **CT15** | Título vazio | Particionamento |
| **CT16** | Editar filme | Tabela de Decisão |
| **CT17** | Editar inválido | Tabela de Decisão |
| **CT18** | Remover filme | Transição de Estados |
| **CT19** | Acesso sem autenticação| Transição de Estados |
| **CT20** | Logout | Transição de Estados |

**Total:** 20 casos de teste manuais.

## 11. Matriz de rastreabilidade

| Requisito | Descrição | Casos de teste |
| :--- | :--- | :--- |
| **RF01** | Cadastro de usuário | CT01, CT02, CT03, CT04, CT05 |
| **RF02** | Login | CT06, CT07, CT08, CT09 |
| **RF03** | Busca de filmes | CT10, CT11, CT12, CT13 |
| **RF04** | Adicionar filme | CT14, CT15 |
| **RF05** | Editar filme | CT16, CT17 |
| **RF06** | Remover filme | CT18 |
| **RF07** | Autenticação e proteção de recursos | CT19, CT20 |

> A matriz permite verificar quais requisitos possuem cobertura por testes e facilita a identificação de requisitos que não foram contemplados.

---

## 12. Registro de execução
Esta seção deverá ser preenchida durante a execução dos testes.

| ID | Resultado | Evidência | Observação |
| :--- | :--- | :--- | :--- |
| **CT01** | A executar | - | - |
| **CT02** | A executar | - | - |
| **CT03** | A executar | - | - |
| **CT04** | A executar | - | - |
| **CT05** | A executar | - | - |
| **CT06** | A executar | - | - |
| **CT07** | A executar | - | - |
| **CT08** | A executar | - | - |
| **CT09** | A executar | - | - |
| **CT10** | A executar | - | - |
| **CT11** | A executar | - | - |
| **CT12** | A executar | - | - |
| **CT13** | A executar | - | - |
| **CT14** | A executar | - | - |
| **CT15** | A executar | - | - |
| **CT16** | A executar | - | - |
| **CT17** | A executar | - | - |
| **CT18** | A executar | - | - |
| **CT19** | A executar | - | - |
| **CT20** | A executar | - | - |

**Legenda:**
* **Aprovado:** comportamento observado corresponde ao resultado esperado.
* **Reprovado:** comportamento observado não corresponde ao resultado esperado.
* **Bloqueado:** não foi possível executar o teste devido a uma dependência ou problema externo.

---

## 13. Relatório de execução
Após a execução dos testes, deverão ser registrados:
* Quantidade total de testes executados.
* Quantidade de testes aprovados.
* Quantidade de testes reprovados.
* Quantidade de testes bloqueados.
* Percentual de aprovação.
* Defeitos encontrados.
* Evidências dos testes, quando disponíveis.

### Resumo

| Indicador | Resultado |
| :--- | :--- |
| **Total de casos** | 20 |
| **Aprovados** | *A preencher* |
| **Reprovados** | *A preencher* |
| **Bloqueados** | *A preencher* |
| **Defeitos encontrados** | *A preencher* |

---

## 14. Bug Report

> **BUG-001 - [Título do defeito]**  
> **Severidade:** A preencher  
> **Prioridade:** A preencher  
> **Caso de teste relacionado:** CTXX  
> **Data:** A preencher  
> **Ambiente:** Windows 11 / Google Chrome  
>
> **Pré-condição:**  
> Descrever o estado necessário para reproduzir o defeito.
> 
> **Passos para reprodução:**  
> 1. Primeiro passo.
> 2. Segundo passo.
> 3. Terceiro passo.
> 4. Ação que provoca o problema.
> 
> **Resultado esperado:**  
> Descrever o comportamento esperado.
> 
> **Resultado obtido:**  
> Descrever exatamente o comportamento observado.
> 
> **Evidência:**  
> Adicionar screenshot, vídeo ou outra evidência quando disponível.
> 
> **Impacto:**  
> Descrever como o defeito afeta o funcionamento do sistema.

---

## 15. Critérios de aceitação
O sistema será considerado aprovado para os objetivos deste plano quando:
* As funcionalidades críticas apresentarem comportamento conforme especificado.
* Os casos de teste críticos forem aprovados.
* Entradas inválidas forem tratadas adequadamente.
* O sistema não apresentar erros bloqueantes durante os fluxos principais.
* As regras de negócio avaliadas pelas tabelas de decisão forem respeitadas.
* As transições de estado testadas apresentarem comportamento esperado.
* Os defeitos encontrados forem devidamente documentados.

## 16. Conclusão
O presente plano de testes estabelece uma abordagem estruturada para a avaliação funcional do sistema React + NestJS Movies DB.

Foram definidos 20 casos de teste manuais, contemplando as principais funcionalidades do sistema e utilizando quatro técnicas de teste: Particionamento de Equivalência, Análise de Valor Limite, Tabela de Decisão e Transição de Estados.

A matriz de rastreabilidade relaciona os requisitos aos respectivos casos de teste, permitindo avaliar a cobertura funcional. Durante a execução, os resultados deverão ser registrados e os defeitos encontrados deverão ser documentados por meio de bug reports.

Dessa forma, o plano fornece uma base para avaliar sistematicamente o comportamento do sistema e identificar problemas relacionados à validação de entradas, regras de negócio, autenticação, gerenciamento de filmes e integração com serviços externos.