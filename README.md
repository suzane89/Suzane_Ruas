

# 1. Descrição do Sistema

Exercício 1:
O nome da clinica é cachorro amarelo

A seguir temos informações sobre um clinica veterinária

1 Uma clínica veterinária atende apenas os animais: gatos e cachorros. 

2 Os clientes devem fazer um cadastro de si e dos animais. 

3 Os clientes devem informar as condições nas quais os animais chegam. 

4 Os clientes devem informar o tipo de ração que o animal come. 

5 O cliente deve informar hábitos do animal. 
6 Para cada animal é possível que mais de um veterinário o atenda. 

7 Os animais podem chegar e serem atendidos de acordo com uma agenda do dia.

8 Cada animal atendido receberá uma ficha e um prontuário. 

9 Outros donos podem querer marcar horários de atendimento futuro.

10 O atendimento gera uma receita para o animal.

11 Quando um cliente chega na clínica veterinária ele é atendido por um atendente.

12 O atendente deve verificar se existe agenda disponível com um veterinário.

13 O atendente deve colocar o cliente e seu animal na fila de espera, se for o caso. 

14 O atendente deve levar o cliente e o animal até o veterinário. 

15 O veterinário deve realizar uma entrevista com o dono do animal. 

16 O resultado da entrevista deve ir para um formulário. 

17 O veterinário deverá examinar o animal e anotar em prontuário(ficha) suas observações. 

18 Dependendo da situação do animal este receberá uma receita.

19 O horário de Atendimento de Segunda a Sexta das 8 às 18:00 hrs.

20 Todo animal precisa ser pesado assim que chega à clínica.

21 A Clinica tem uma loja de produtos para cães e gatos.

22 A pet shop vende ração, apetrechos,roupas e brinquedos para os pets.

23 A Clinica tem um programa de hospedagem.




# 2. Diagrama de Banco de Dados


```mermaid
erDiagram
    CLIENTE {
        string nome
        string telefone
        string endereco
    }

    ANIMAL {
        string nome
        string especie
        string raca
        string cor
        string tipoRacao
        string habitos
        string condicaoChegada
    }

    VETERINARIO {
        string nome
        string especialidade
    }

    ATENDENTE {
        string nome
    }

    PRONTUARIO {
        string observacoes
        string receita
    }

    FORMULARIO {
        string resultadoEntrevista
    }

    AGENDA {
        datetime dataHora
        boolean disponivel
    }

    PRODUTO {
        string tipo
        string descricao
    }

    HOSPEDAGEM {
        string descricao
        datetime dataInicio
        datetime dataFim
    }

    CLIENTE ||--o{ ANIMAL : possui
    ANIMAL ||--o{ PRONTUARIO : gera
    ANIMAL ||--o{ FORMULARIO : gera
    ANIMAL ||--o{ AGENDA : agenda
    VETERINARIO ||--o{ ANIMAL : atende
    ATENDENTE ||--o{ CLIENTE : atende
    CLIENTE ||--o{ HOSPEDAGEM : reserva
    PRODUTO ||--o{ CLIENTE : compra



```


# 3. Diagrama de Casos de Uso

![https://github.com/suzane89/Suzane_Ruas/blob/main/Casos%20de%20Uso.drawio.png](https://github.com/suzane89/Suzane_Ruas/blob/main/Casos%20de%20Uso.drawio.png)

# 4. Principais Telas do Sistema

# 5. Arquitetura de Sistema

```mermaid
graph TD;

    %% Definição de Contêineres
    subgraph WebClient [Cliente Web]
        Browser[Browser]
    end
    
    subgraph MobileClient [Cliente Mobile]
        MobileApp[Aplicativo Mobile]
    end
    
    subgraph GHPC [Aplicação GHP]
        WebApp[Aplicação Web]
    end
    
    subgraph API [API REST]
        VeterinarioAPI[API Veterinários]
        ClienteAPI[API Clientes]
        AgendamentoAPI[API Agendamento]
        AtendimentoAPI[API Atendimento]
    end
    
    subgraph Database [Servidor de Banco de Dados]
        ClientesDB[(Clientes DB)]
        AnimaisDB[(Animais DB)]
        AgendamentosDB[(Agendamentos DB)]
        FichasDB[(Fichas e Prontuários DB)]
    end
    
    %% Definição de Fluxos de Informação
    Browser --> |HTTP Request| WebApp
    MobileApp --> |API Request| VeterinarioAPI
    
    WebApp --> |Consulta| VeterinarioAPI
    WebApp --> |Consulta| ClienteAPI
    WebApp --> |Consulta| AgendamentoAPI
    WebApp --> |Consulta| AtendimentoAPI
    
    VeterinarioAPI --> |Consulta/Atualização| ClientesDB
    ClienteAPI --> |Consulta/Atualização| ClientesDB
    AgendamentoAPI --> |Consulta/Atualização| AgendamentosDB
    AtendimentoAPI --> |Consulta/Atualização| FichasDB
    
    VeterinarioAPI --> |Consulta| AnimaisDB
    ClienteAPI --> |Consulta| AnimaisDB
    
    VeterinarioAPI --> |Atualização| FichasDB

```

