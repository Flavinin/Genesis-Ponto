
# 📋 Product Backlog — Gênesis Ponto

**Projeto:** Gênesis Ponto  
**Empresa:** Gênesis Suprimentos  
**Projeto Integrado Multidisciplinar (PIM) — UNIP**

---

## 1. Requisitos Funcionais (RF)

Os requisitos funcionais descrevem as funcionalidades que o sistema deve oferecer aos usuários, considerando os diferentes níveis de acesso.

| Código | Descrição do Requisito |
|---|---|
| **RF01** | O sistema deve permitir o cadastro de usuários, registrando matrícula, nome, senha e perfil de acesso (ADM, Gerente ou Funcionário). |
| **RF02** | O sistema deve permitir realizar login por matrícula e senha, apresentando menus e funcionalidades conforme o perfil do usuário. |
| **RF03** | O sistema deve permitir registrar os horários de entrada, saída para intervalo, retorno do intervalo e saída final da jornada. |
| **RF04** | O sistema deve permitir consultar a lista de usuários cadastrados e seus respectivos perfis, respeitando as permissões de acesso. |
| **RF05** | O sistema deve permitir consultar o histórico de registros de ponto, apresentando data, horário e tipo de marcação. |
| **RF06** | O sistema deve calcular o total de horas trabalhadas com base nos registros de ponto, descontando os intervalos. |
| **RF07** | O sistema deve gerar um resumo de frequência, apresentando dias trabalhados, atrasos e horas extras. |

---

## 2. Requisitos Não Funcionais (RNF)

Os requisitos não funcionais estabelecem as características técnicas, padrões de qualidade e condições de funcionamento do sistema.

| Código | Descrição do Requisito |
|---|---|
| **RNF01** | O sistema deve ser desenvolvido em linguagem C e executado por meio do terminal. |
| **RNF02** | O sistema deve apresentar menus e mensagens em português claro, com opções organizadas conforme o perfil do usuário. |
| **RNF03** | O sistema deve validar os dados informados, evitando entradas inválidas e apresentando mensagens de erro compreensíveis. |
| **RNF04** | O código deve ser organizado em funções e estruturas de dados, facilitando sua manutenção e compreensão. |
| **RNF05** | O sistema deve armazenar e recuperar informações de usuários e registros de ponto por meio de arquivos TXT. |
| **RNF06** | O sistema deve registrar automaticamente os horários, utilizando a biblioteca time.h, e apresentar datas em formato padronizado. |
| **RNF07** | O sistema deve controlar o acesso às funcionalidades conforme o perfil autenticado e manter consistência nos cálculos de horas, atrasos e horas extras. |

---

## 3. Regras de Negócio (RN)

As regras de negócio estabelecem as condições e restrições que devem ser respeitadas durante o funcionamento do sistema.

| Código | Descrição da Regra de Negócio |
|---|---|
| **RN01** | Cada usuário deve possuir uma matrícula única e uma senha para acessar o sistema. |
| **RN02** | Somente o Administrador (ADM) pode cadastrar usuários e definir seus perfis de acesso. |
| **RN03** | O Gerente pode consultar informações dos usuários, enquanto o Funcionário pode visualizar exclusivamente seus próprios registros. |
| **RN04** | Todos os usuários autenticados podem registrar o próprio ponto, respeitando a sequência: entrada, saída para intervalo, retorno e saída final. |
| **RN05** | O cálculo das horas trabalhadas deve considerar apenas jornadas com os quatro registros completos, descontando o período de intervalo. |
| **RN06** | O sistema deve considerar como atraso entradas realizadas após as 09h00 e contabilizar horas extras quando a jornada ultrapassar 8 horas diárias. |
| **RN07** | O sistema deve permitir o acesso somente com matrícula e senha válidas, impedindo operações não autorizadas conforme o perfil do usuário. |

---

## 4. Matriz de Permissões

| Funcionalidade | ADM | Gerente | Funcionário |
|---|:---:|:---:|:---:|
| Realizar login | Sim | Sim | Sim |
| Cadastrar usuários | Sim | Não | Não |
| Listar usuários | Sim | Sim | Não |
| Registrar o próprio ponto | Sim | Sim | Sim |
| Consultar próprio histórico | Sim | Sim | Sim |
| Consultar histórico de outros usuários | Sim | Sim | Não |
| Calcular horas trabalhadas | Sim | Sim | Sim |
| Consultar resumo de frequência | Sim | Sim | Sim |

---

## 5. Resumo dos Requisitos

| Categoria | Quantidade |
|---|---:|
| Requisitos Funcionais (RF) | 7 |
| Requisitos Não Funcionais (RNF) | 7 |
| Regras de Negócio (RN) | 7 |
| **Total** | **21** |

---

## 6. Considerações Finais

A atualização do Product Backlog foi realizada considerando as melhorias implementadas no sistema Gênesis Ponto durante a Sprint 03.

Os requisitos foram reorganizados para contemplar a autenticação de usuários, os três níveis de acesso, o registro de ponto, o cálculo de horas trabalhadas e o resumo de frequência.

Essa atualização permite manter a documentação mais objetiva e alinhada ao funcionamento do protótipo desenvolvido em linguagem C.

---

**Projeto Gênesis Ponto — UNIP | 2026**
