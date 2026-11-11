# 💻 GENESIS PONTO
### Documentação do Código-Fonte

**Projeto Integrado Multidisciplinar (PIM) — UNIP**

O **Genesis Ponto** é um protótipo de sistema de controle de ponto eletrônico desenvolvido em linguagem C para a empresa Gênesis Suprimentos.

O projeto tem como objetivo facilitar o gerenciamento dos funcionários, automatizar o registro de horários e permitir o acompanhamento das jornadas de trabalho.

O sistema possui três níveis de acesso: **Administrador (ADM), Gerente e Funcionário**, cada um com permissões específicas.

---

## 🛠️ 1. Tecnologias Utilizadas

| Tecnologia | Utilização |
|---|---|
| Linguagem C | Desenvolvimento do sistema |
| Visual Studio Code | Ambiente de programação |
| GitHub | Versionamento e armazenamento do código |
| Arquivos TXT | Armazenamento dos usuários e registros |
| Terminal | Interface de interação com o usuário |

O sistema funciona diretamente no terminal, utilizando menus numéricos para acessar suas funcionalidades.

---

## 📚 2. Bibliotecas Utilizadas

O código utiliza cinco bibliotecas da linguagem C.

| Biblioteca | Finalidade |
|---|---|
| `stdio.h` | Entrada e saída de dados |
| `stdlib.h` | Conversão de valores e controle de execução |
| `string.h` | Manipulação e comparação de textos |
| `time.h` | Registro e cálculo de horários |

### Biblioteca stdio.h

```c
#include <stdio.h>
```

Responsável pelas operações de entrada e saída de dados, permitindo a comunicação entre o usuário e o programa.

**Principais funções utilizadas:**

- `printf()` — Exibe mensagens no terminal.
- `puts()` — Exibe mensagens com quebra de linha.
- `fgets()` — Lê textos digitados pelo usuário.
- `fprintf()` — Escreve informações nos arquivos.
- `fscanf()` — Lê informações armazenadas nos arquivos.
- `fopen()` — Abre arquivos.
- `fclose()` — Fecha arquivos.

**Exemplo:**

```c
printf("Matricula: ");
```

Esse comando solicita que o usuário informe sua matrícula.

### Biblioteca stdlib.h

```c
#include <stdlib.h>
```

Utilizada para operações gerais do programa.

**Principais funções:**

- `strtol()` — Converte uma sequência de caracteres em número inteiro.
- `exit()` — Encerra a execução do programa.

**Exemplo:**

```c
if (!fgets(s, sizeof(s), stdin))
    exit(0);
```

Nesse trecho, caso não seja possível continuar a leitura da entrada, o programa é encerrado.

### Biblioteca string.h

```c
#include <string.h>
```

Responsável pela manipulação de textos e pela comparação de informações.

**Principais funções:**

- `strcmp()` — Compara duas strings.
- `strcpy()` — Copia uma string para outra.
- `strlen()` — Retorna o tamanho de uma string.
- `strchr()` — Procura um caractere dentro de uma string.
- `strcspn()` — Localiza a posição do primeiro caractere pertencente a um conjunto informado.

**Exemplo:**

```c
strcmp(usuarios[id].senha, senha) == 0
```

Esse comando verifica se a senha digitada corresponde à senha cadastrada.

Quando `strcmp()` retorna zero, significa que as duas strings são iguais.

### Biblioteca time.h

```c
#include <time.h>
```

Utilizada para registrar automaticamente os horários dos funcionários e realizar cálculos relacionados à jornada de trabalho.

**Principais funções:**

- `time()` — Obtém o horário atual do sistema.
- `localtime()` — Converte o horário para data e hora locais.
- `difftime()` — Calcula a diferença entre dois horários.

**Exemplo:**

```c
time_t agora = time(NULL);
```

O comando obtém o horário atual do computador e o armazena na variável `agora`.

Dessa maneira, o funcionário não precisa digitar manualmente o horário de entrada ou saída.

---

## 📋 3. Requisitos Funcionais

| Código | Funcionalidade |
|---|---|
| RF01 | Cadastrar funcionários |
| RF02 | Listar funcionários |
| RF03 | Registrar entrada |
| RF04 | Registrar saída para intervalo e retorno |
| RF05 | Registrar saída final |
| RF06 | Calcular horas trabalhadas |
| RF07 | Gerar resumo de frequência |

Além dos requisitos apresentados, o protótipo possui autenticação por matrícula e senha, permitindo o controle de acesso conforme o perfil do usuário.

---

## 👥 4. Tipos de Usuários

O sistema possui três perfis, identificados por números inteiros.

| Identificador | Perfil | Permissões |
|---|---|---|
| 1 | ADM | Cadastrar usuários, registrar o próprio ponto e consultar informações |
| 2 | Gerente | Listar usuários, registrar o próprio ponto e consultar informações |
| 3 | Funcionário | Registrar o próprio ponto e consultar suas informações |

### Administrador (ADM)

Possui o maior nível de acesso ao sistema.

É responsável pelo cadastro de usuários e pela definição de seus respectivos perfis.

Também pode consultar o histórico de ponto, as horas trabalhadas e os resumos de frequência.

### Gerente

É responsável pelo acompanhamento dos funcionários.

Pode listar os usuários cadastrados, consultar registros de ponto, verificar jornadas de trabalho e identificar atrasos e horas extras.

Não possui permissão para cadastrar novos usuários.

### Funcionário

Possui acesso limitado às próprias informações.

Pode registrar os horários da jornada, consultar seu histórico, verificar as horas trabalhadas e visualizar seu resumo de frequência.

Não pode consultar os dados dos demais usuários.

---

## 🧱 5. Estruturas de Dados

O código utiliza `struct` para organizar as informações dos usuários e dos registros de ponto.

Uma `struct` permite reunir diferentes tipos de dados em uma única estrutura.

### Estrutura Usuario

```c
typedef struct {
    int matricula, perfil;
    char nome[50], senha[30];
} Usuario;
```

**Explicação:**

- `int matricula` — Armazena a matrícula do usuário.
- `int perfil` — Identifica seu nível de acesso.
- `char nome[50]` — Armazena o nome, com capacidade para até 49 caracteres e o terminador nulo.
- `char senha[30]` — Armazena a senha, com capacidade para até 29 caracteres e o terminador nulo.

O comando `typedef` permite utilizar o nome `Usuario` diretamente na declaração de variáveis.

### Estrutura Registro

```c
typedef struct {
    int matricula, tipo;
    time_t hora;
} Registro;
```

**Explicação:**

- `matricula` — Identifica o funcionário responsável pelo registro.
- `tipo` — Identifica o tipo de marcação realizada.
- `hora` — Armazena a data e o horário do registro.

### Vetores utilizados

```c
Usuario usuarios[MAX];
Registro registros[MAX];

int nu = 0, nr = 0;
```

O código utiliza dois vetores para armazenar temporariamente os dados.

| Variável | Função |
|---|---|
| `usuarios[MAX]` | Armazena os usuários |
| `registros[MAX]` | Armazena os registros de ponto |
| `nu` | Quantidade de usuários cadastrados |
| `nr` | Quantidade de registros realizados |

A constante `MAX` possui valor 1000, estabelecendo o limite de cada vetor.

---

## ⚙️ 6. Funções do Sistema

O código é organizado em funções para facilitar sua compreensão, manutenção e reutilização.

### Função numero()

```c
int numero(char *msg)
```

Responsável por solicitar e ler valores numéricos digitados pelo usuário.

Utiliza `fgets()` para receber a entrada e `sscanf()` para interpretar o número informado.

Essa função é utilizada principalmente na seleção das opções dos menus e na leitura das matrículas.

### Função texto()

```c
void texto(char *msg, char *s, int tam)
```

Responsável pela leitura de informações textuais, como nomes e senhas.

Também verifica algumas condições de validade, impedindo campos vazios, textos acima do limite definido e a utilização do caractere `;`, empregado como separador nos arquivos.

### Função buscar()

```c
int buscar(int mat)
```

Procura um usuário por sua matrícula.

O programa percorre o vetor de usuários utilizando uma estrutura de repetição `for`.

Caso encontre a matrícula, retorna a posição do usuário no vetor.

Caso contrário, retorna `-1`.

**Exemplo:**

```c
if (buscar(u.matricula) >= 0)
```

Essa verificação permite identificar matrículas já cadastradas, evitando duplicidades.

### Função salvar()

```c
void salvar()
```

Responsável por armazenar as informações nos arquivos de texto.

São utilizados dois arquivos:

- `usuarios.txt` — Matrícula, perfil, nome e senha.
- `registros.txt` — Matrícula, tipo de registro e horário.

O programa utiliza `fopen()` no modo `"w"`, que cria ou sobrescreve o arquivo, e `fprintf()` para gravar as informações.

Após a gravação, utiliza `fclose()` para fechar o arquivo.

### Função carregar()

```c
void carregar()
```

Responsável por recuperar as informações armazenadas anteriormente.

Ao iniciar o sistema, essa função abre os arquivos no modo `"r"` e utiliza `fscanf()` para ler os dados.

As informações são transferidas para os vetores do programa.

Assim, os usuários e registros podem continuar disponíveis após o encerramento e a reabertura do sistema.

### Função cadastrar()

```c
void cadastrar(int primeiro)
```

Responsável pelo cadastro de novos usuários.

Durante o cadastro, o programa solicita matrícula, nome, senha e perfil de acesso.

Também verifica se a matrícula é válida e se já existe no sistema.

O parâmetro `primeiro` identifica se o cadastro corresponde ao administrador inicial.

Quando `primeiro` recebe o valor 1, o usuário é cadastrado automaticamente com o perfil ADM.

### Função listar()

```c
void listar()
```

Percorre o vetor de usuários cadastrados e apresenta suas informações no terminal.

Exibe a matrícula, o nome e o perfil de cada usuário.

Essa função pode ser utilizada pelo administrador e pelo gerente.

### Função mesmoDia()

```c
int mesmoDia(time_t a, time_t b)
```

Responsável por verificar se dois horários pertencem ao mesmo dia.

Utiliza `localtime()` para converter os horários e compara o ano e o dia do ano.

É utilizada para organizar corretamente os registros de ponto de cada jornada.

### Função registrar()

```c
void registrar(int mat)
```

Responsável por registrar os horários da jornada de trabalho.

O sistema disponibiliza quatro tipos de marcação:

| Código | Registro |
|---|---|
| 1 | Entrada |
| 2 | Saída para intervalo |
| 3 | Retorno do intervalo |
| 4 | Saída final |

A função utiliza `time(NULL)` para obter o horário atual.

Também verifica a sequência dos registros realizados durante o dia.

**Exemplo:**

O funcionário precisa registrar a entrada antes de realizar a saída para intervalo.

Caso tente registrar uma marcação fora da sequência esperada, o programa apresenta uma mensagem de erro.

Após a validação, o registro é armazenado no vetor e salvo no arquivo `registros.txt`.

### Função consultar()

```c
void consultar(int mat, int op)
```

Responsável pela consulta dos registros, cálculo das horas trabalhadas e apresentação do resumo de frequência.

A função utiliza o parâmetro `op` para identificar a operação solicitada.

| Opção | Resultado |
|---|---|
| 4 | Exibe histórico de ponto |
| 5 | Calcula dias e horas trabalhadas |
| 6 | Apresenta resumo de frequência |

**Cálculo das horas trabalhadas**

O sistema calcula o tempo entre a entrada e a saída para intervalo, somando ao tempo entre o retorno do intervalo e a saída final.

```c
double h = (difftime(t[1], t[0]) +
            difftime(t[3], t[2])) / 3600.0;
```

A função `difftime()` retorna a diferença entre os horários em segundos.

O resultado é dividido por 3600 para converter os segundos em horas.

**Exemplo:**

| Registro | Horário |
|---|---|
| Entrada | 08:00 |
| Saída para intervalo | 12:00 |
| Retorno do intervalo | 13:00 |
| Saída final | 17:00 |

O programa calcula:

- Primeiro período: 4 horas.
- Segundo período: 4 horas.
- Total trabalhado: **8 horas**.

O intervalo de uma hora não é contabilizado.

**Cálculo de horas extras**

```c
if (h > 8)
    extras += h - 8;
```

Caso o funcionário trabalhe mais de 8 horas em um dia, o tempo excedente será contabilizado como hora extra.

**Identificação de atrasos**

```c
if (d.tm_hour * 60 + d.tm_min > 540)
    atrasos++;
```

O programa converte o horário de entrada em minutos.

O número 540 representa 9 horas multiplicadas por 60 minutos.

Assim, entradas após as 09:00 são contabilizadas como atraso.

**Observação:** o protótipo considera uma jornada de referência fixa, com entrada até as 9h e limite de 8 horas diárias para o cálculo de horas extras. Essas regras não são configuradas individualmente.

### Função menu()

```c
void menu(int id)
```

Responsável por apresentar as funcionalidades disponíveis conforme o perfil do usuário.

A função utiliza estruturas condicionais `if` e `else if` para verificar as permissões.

O administrador visualiza todas as opções, enquanto o gerente não possui acesso ao cadastro de usuários.

O funcionário pode registrar e consultar apenas seus próprios pontos.

### Função main()

```c
int main()
```

É a função principal do programa, responsável por iniciar o sistema e controlar sua execução.

Primeiramente, chama `carregar()` para recuperar os dados.

Caso não exista nenhum usuário cadastrado, solicita a criação do administrador inicial.

Em seguida, apresenta a tela de login.

Após validar a matrícula e a senha informadas, chama a função `menu()` para apresentar as opções disponíveis ao usuário autenticado.

---

## 🔐 7. Funcionamento do Login

O sistema solicita a matrícula e a senha cadastradas.

```text
=== LOGIN GENESIS PONTO ===

1 - Entrar
0 - Sair

Opcao: 1

Matricula: 100
Senha: 1234
```

O programa utiliza a função `buscar()` para localizar a matrícula e `strcmp()` para comparar a senha digitada com a senha armazenada.

Caso as informações estejam corretas, o usuário acessa seu menu.

Caso contrário, o sistema apresenta a mensagem:

```text
Matricula ou senha incorreta!
```

**Limitação do protótipo:** as senhas são armazenadas em texto simples no arquivo `usuarios.txt`. Para uma versão de produção, seria necessário implementar armazenamento seguro de senhas e medidas adicionais de autenticação.

---

## 🖥️ 8. Menus do Sistema

### Menu do Administrador

```text
===== GENESIS PONTO | ADM =====

1 - Cadastrar usuario
2 - Listar usuarios
3 - Registrar meu ponto
4 - Consultar historico
5 - Calcular horas
6 - Resumo de frequencia
0 - Sair da conta
```

### Menu do Gerente

```text
===== GENESIS PONTO | GERENTE =====

2 - Listar usuarios
3 - Registrar meu ponto
4 - Consultar historico
5 - Calcular horas
6 - Resumo de frequencia
0 - Sair da conta
```

### Menu do Funcionário

```text
===== GENESIS PONTO | FUNCIONARIO =====

3 - Registrar meu ponto
4 - Consultar historico
5 - Calcular horas
6 - Resumo de frequencia
0 - Sair da conta
```

Os menus são apresentados conforme o nível de acesso de cada usuário.

---

## 📂 9. Estrutura do Projeto

```text
Genesis-PIM/
└── CODIGO/
    ├── CODIGO.md
    ├── main.c
    ├── usuarios.txt
    └── registros.txt
```

| Arquivo | Descrição |
|---|---|
| `main.c` | Código-fonte do sistema |
| `CODIGO.md` | Documentação do projeto |
| `usuarios.txt` | Armazenamento dos usuários |
| `registros.txt` | Armazenamento dos registros de ponto |

Os arquivos `.txt` são criados pelo sistema durante a utilização, caso seja possível gravá-los no diretório de execução.

---

## 🔄 10. Fluxo de Funcionamento

O sistema segue a seguinte sequência:

1. **Inicialização:** o programa carrega os dados armazenados nos arquivos.
2. **Primeiro acesso:** caso não existam usuários cadastrados, solicita a criação do ADM.
3. **Login:** solicita matrícula e senha.
4. **Validação:** verifica se o usuário existe e se a senha está correta.
5. **Identificação do perfil:** determina se o usuário é ADM, Gerente ou Funcionário.
6. **Menu:** apresenta as funcionalidades correspondentes ao perfil.
7. **Operações:** permite cadastrar, consultar ou registrar pontos conforme as permissões.
8. **Armazenamento:** salva as alterações nos arquivos de texto.
9. **Encerramento:** permite sair da conta ou encerrar o programa.

---

## 🧠 11. Conceitos de Programação Utilizados

| Conceito | Aplicação no sistema |
|---|---|
| Variáveis | Armazenamento de matrículas, perfis e contadores |
| Constantes | Definição do limite de registros com `#define MAX` |
| Vetores | Armazenamento dos usuários e registros |
| Struct | Organização das informações |
| Funções | Divisão das funcionalidades do sistema |
| Condicionais | Validação de dados e permissões |
| Laços de repetição | Percorrer registros e apresentar menus |
| Strings | Armazenamento de nomes e senhas |
| Arquivos | Persistência de informações em TXT |
| Manipulação de tempo | Registro e cálculo de jornadas |

Esses conceitos permitem organizar o sistema de maneira modular, facilitando a compreensão do código e futuras alterações.

---

## ⚠️ 12. Limitações do Protótipo

Por se tratar de um projeto acadêmico, o sistema apresenta algumas limitações:

- Utiliza uma interface de terminal, sem elementos gráficos.
- Armazena as senhas em texto simples.
- Trabalha com um limite máximo de 1000 usuários e 1000 registros em memória.
- Considera o horário de entrada até as 09:00 como referência para atrasos.
- Considera horas extras apenas após 8 horas trabalhadas no dia.
- Realiza os cálculos somente quando os quatro registros do dia estão completos.
- Não possui recuperação de senha.
- Não importa automaticamente cadastros de versões anteriores que utilizavam outro formato de arquivo.

Essas características não impedem a demonstração das funcionalidades principais, mas precisam ser consideradas antes de uma aplicação em ambiente empresarial.

---

## 🚀 13. Melhorias Futuras

Para futuras versões do Gênesis Ponto, podem ser implementadas as seguintes melhorias:

- Desenvolvimento de interface gráfica.
- Integração com banco de dados.
- Armazenamento seguro de senhas.
- Recuperação de senha.
- Cadastro de jornadas individuais.
- Geração de relatórios em PDF.
- Exportação de relatórios para planilhas.
- Consulta de frequência por período.
- Identificação de faltas e justificativas.
- Desenvolvimento de uma versão web ou aplicativo.

---

## ✅ 14. Conclusão

O **Gênesis Ponto** foi desenvolvido com o objetivo de apresentar uma solução inicial para o gerenciamento de funcionários e o controle de jornadas de trabalho da empresa Gênesis Suprimentos.

Por meio da linguagem C, o sistema permite cadastrar usuários, definir níveis de acesso, registrar horários de entrada e saída, consultar históricos e calcular horas trabalhadas.

A utilização de estruturas de dados, funções, condicionais, vetores e manipulação de arquivos demonstra a aplicação prática dos conhecimentos adquiridos durante o curso.

Embora seja um protótipo acadêmico, o projeto apresenta uma base funcional que poderá ser aprimorada futuramente com recursos de segurança, banco de dados e interfaces mais modernas.

---

**Genesis Ponto — Projeto Integrado Multidisciplinar (PIM) — UNIP**
