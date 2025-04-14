# oficina-spring-boot
# 1. Testes de Caixa Preta

Realização do teste como se fosse um usuário comum, testando as entradas e saídas pelo Postman (ou Swagger) com o objetivo de verificar se o endpoint funciona corretamente, tanto com dados válidos quanto com dados inválidos.

## CP 01
- **Funcionalidade:** Cadastro com dados válidos  
- **Entrada de Teste:** Nome, e-mail e senha (válidos)  
- **Resultado Esperado:** Sucesso na criação  
- **Resultado Obtido:** Usuário criado com sucesso  
- **Status:** Aprovado ✅  

## CP 02
- **Funcionalidade:** Cadastro com senha vazia  
- **Entrada de Teste:** Campo “senha” vazio  
- **Resultado Esperado:** Mensagem de erro  
- **Resultado Obtido:** Usuário criado normalmente  
- **Status:** Reprovado ❌  

## CP 03
- **Funcionalidade:** Cadastro com e-mail sem @  
- **Entrada de Teste:** E-mail mal formatado (gustavo-aula-qafaseh.com.br)  
- **Resultado Esperado:** Mensagem de erro  
- **Resultado Obtido:** Usuário criado normalmente  
- **Status:** Reprovado ❌  

## CP 04
- **Funcionalidade:** Confirmação de senha  
- **Entrada de Teste:** Verificação se as duas senhas coincidem  
- **Resultado Esperado:** API deveria exigir confirmação de senha  
- **Resultado Obtido:** Campo não solicitado  
- **Status:** Incompleto ⚠️  

## CP 05
- **Funcionalidade:** Login com dados válidos  
- **Entrada de Teste:** E-mail e senha corretos  
- **Resultado Esperado:** Token JWT  
- **Resultado Obtido:** Token recebido  
- **Status:** Aprovado ✅  

## CP 06
- **Funcionalidade:** Login com dados inválidos  
- **Entrada de Teste:** E-mail correto e senha inválida  
- **Resultado Esperado:** Erro de autenticação  
- **Resultado Obtido:** Retorno de erro  
- **Status:** Aprovado ✅  

## CP 07
- **Funcionalidade:** Headers Desconfigurados  
- **Entrada de Teste:** Headers ausentes ou com erro  
- **Resultado Esperado:** Bloqueio da requisição  
- **Resultado Obtido:** Retorno de erro  
- **Status:** Aprovado ✅  

## CP 08
- **Funcionalidade:** Acesso com token inválido  
- **Entrada de Teste:** Header Authorization com token aleatório ou vencido  
- **Resultado Esperado:** Erro de autenticação  
- **Resultado Obtido:** Retorno de erro  
- **Status:** Aprovado ✅  

---

# 2. Testes de Caixa Branca

## AutenticacaoService.java

### `loadUserByUsername(String email)`
- Carrega o usuário pelo e-mail a partir do repositório  
  - **Usuário Existente:** Retorna `UserDetails`  
  - **Usuário Inexistente:** Retorna `UsernameNotFoundException("Dados de usuário e senha são inválidos!")`  

## TokenService.java

### `gerarToken(Authentication authentication)`
- Geração do token JWT com base no usuário autenticado  
  - **Authentication válido:** Retorna token JWT  
  - **Usuário sem ID:** Erro ao gerar token  

### `tokenEhValido(String token)`
- Verifica se o token JWT é válido  
  - **Token correto:** Retorna `true`  
  - **Token inválido:** Retorna `false`  

### `getIdUsuario(String token)`
- Extrai o ID do usuário a partir do token JWT  
  - **Token válido com ID numérico:** Retorna ID  
  - **Token inválido:** Lança exceção  

## UserService.java

### `criar(User dto)`
- Codifica a senha e salva o usuário  
  - **Senha válida:** Criptografa e salva  
  - **Senha nula ou vazia:** Comportamento indefinido ou exceção  

### `alterar(User dto)`
- Atualiza os dados do usuário  
  - **Usuário existente:** Atualiza  
  - **Usuário inexistente:** Sobrescreve ou cria novo  

### `apagar(Long id)`
- Deleta o usuário a partir do ID  
  - **ID existente:** Remove usuário  
  - **ID inexistente:** `NoSuchElementException`  

### `buscarUsuario(Long id)`
- Busca um usuário por ID  
  - **ID existente:** Retorna usuário  
  - **ID inexistente:** `NoSuchElementException`  

### `buscarTodos()`
- Retorna todos os usuários  
  - **Com usuários:** Retorna lista  
  - **Sem usuários:** Retorna lista vazia  

---

# 3. Edições no Código

- **Correção da URL:**  
  - De: `150.230.88.104:3306`  
  - Para: `cleberleao.com:3306/cleberleao_oficina`  

- **Correção do usuário:**  
  - De: `root`  
  - Para: `cleberleao_oficina`
  - 
