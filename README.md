# Minishell

> _"fazendo a minha propria tela preta"_

## 🧠 O que é o Minishell?

O **Minishell** é o projeto mais desafiador que desenvolvi até o momento que escrevo esse read durante a minha formação da 42, ele consiste em criar um interpretador de comandos simples (por isso "mini"), inspirado no Bash.
Seu principal objetivo é aprofundar os conhecimentos sobre:

- Processos e sinais
- Manipulação de arquivos e descritores
- Redirecionamentos
- Pipes
- Parsing de entrada
- Execução de binários e built-ins
- Gestão de memória e variáveis de ambiente

---

## 📜 Regras para resolução do problema

- O projeto deve ser escrito em **C**, seguindo a **Norma da 42**.
- Todas as **alocações dinâmicas** devem ser tratadas corretamente, **sem vazamentos de memória**.
- É permitida **apenas uma variável global**, e ela deve ser usada para armazenar **exclusivamente o número de um sinal**.
- A função `readline()` pode vazar memória, mas **o código próprio não pode**.
- O `Makefile` deve conter as regras obrigatórias: `$(NAME)`, `all`, `clean`, `fclean`, `re`.
- Caso use a `libft`, ela deve ser copiada para uma pasta `libft/` com seu próprio Makefile.
- Apenas o conteúdo presente no **repositório Git** será avaliado.
- O bônus **só será avaliado** se a parte obrigatória estiver **completamente funcional**.

---

## 🧩 Como resolvemos o problema

Fazendo a descrição

### 🔧 Funcionalidades implementadas

- Prompt interativo com histórico (`readline`)
- Execução de comandos com base no `$PATH`
- Suporte a redirecionamentos:
  - `>` saída
  - `>>` saída em append
  - `<` entrada
  - `<<` heredoc
- Expansão de variáveis: `$VAR` e `$?`
- Execução de múltiplos comandos com **pipes**
- Tratamento de **aspas simples e duplas**
- Comportamento de sinais:
  - `Ctrl+C`: nova linha com prompt
  - `Ctrl+D`: encerra o shell
  - `Ctrl+\`: ignorado

### ⚙️ Built-ins

- `echo` (com suporte à flag `-n`)
- `cd` (com caminhos relativos ou absolutos)
- `pwd`
- `export`
- `unset`
- `env`
- `exit`

### ✨ Bônus (se aplicável)

- Execução condicional com `&&` e `||`
- Agrupamento com `()`
- Suporte a `wildcards` (`*`) no diretório atual

---

## 🧪 Como testar o projeto

### Clone o repositório

bash
git clone https://github.com/seu-usuario/minishell.git
cd minishell
make

## Execute o shell

./minishell
Você verá algo como:
minishell$

## 3. Exemplos de comandos

echo Hello World
echo $USER
ls -l | grep .c
cat << EOF
linha 1
linha 2
EOF
export TEST=42
echo $TEST

## 4. Testando sinais
Pressione Ctrl+C: o shell deve exibir um novo prompt.

Pressione Ctrl+D: o shell deve ser encerrado.

Pressione Ctrl+\: não deve ocorrer nenhuma ação.

## 5. Verificando vazamentos de memória
Use o seguinte comando para rodar o valgrind e ja suprimir a lib readline:

valgrind --leak-check=full --show-leak-kinds=all --gen-suppressions=all ./minishell
⚠️ Observação: a função readline() pode gerar falsos positivos. Temos que certificar que nosso código próprio esteja livre de vazamentos e a lib readline() podemos apenas ignorar.
