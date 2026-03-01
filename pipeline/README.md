# 🚀 Microsoft Fabric – Curso Prático de Arquitetura Lakehouse

![Microsoft Fabric](https://img.shields.io/badge/Microsoft-Fabric-blue)
![Lakehouse](https://img.shields.io/badge/Architecture-Lakehouse-green)
![Delta](https://img.shields.io/badge/Format-Delta%20Lake-orange)
![Medallion](https://img.shields.io/badge/Pattern-Medallion-purple)

---

![Lab](/images/pipeline-arc.png)


# 📌 Criando Nosso Pipeline End-to-End


![Lab](/images/notebook05.png)

Nesta etapa do curso, vamos construir o fluxo completo:

1. 📥 Ingestão para Bronze  
2. 🔄 Transformação para Silver  
3. ⭐ Modelagem para Gold (Modelo Estrela)  
4. 📊 Criação do Modelo Semântico  
5. 📈 Construção de Relatórios  
6. 🔁 Orquestração com Pipeline  


# 🥉 1. Notebook – `NB_Get_Data_To_Bronze`

## Criando o Notebook

![Lab](/images/notebook05.png)

## Inserindo a fonte de dados Lakehouse

Selecione o Lakehouse correspondente para a camada Bronze.

![Lab](/images/notebook06.png)

> O código do notebook `NB_Get_Data_To_Bronze` está disponível no repositório Git do curso.

---
# 🥈 2. Criando o Lakehouse `Silver`

![Lab](/images/lakehouse10.png)

## Criando o Notebook `NB_Bronze_To_Silver`

Após criar o notebook, vincule a fonte de dados do Lakehouse Silver.

![Lab](/images/notebook07.png)

Nesta etapa realizamos:

- Conversão de tipos  
- Padronização de dados  
- Upsert com MERGE  
- Preparação para modelagem  

---

# 🥇 3. Criando o Lakehouse `Gold`

![Lab](/images/lakehouse11.png)

## Criando o Notebook `NB_Silver_To_Gold`

Vincule o Lakehouse Gold como fonte de dados.

---

## ⭐ Modelo Estrela na Camada Gold

Nesta etapa criamos:

- Tabela Fato  
- Tabelas Dimensão  

![Lab](/images/modelo.png)

A camada Gold representa a estrutura analítica pronta para consumo.

---

# 📊 4. Criando o Modelo Semântico

## 📌 O que é Modelo Semântico?

Um Modelo Semântico é uma camada lógica que organiza os dados técnicos em uma estrutura orientada ao negócio.

Ele transforma:

- Tabelas técnicas  
- Colunas físicas  
- Chaves e joins  

em:

- Conceitos de negócio  
- Métricas  
- Indicadores  
- Relacionamentos compreensíveis  

---
## Criando o Modelo no Lakehouse Gold

Clique no ícone de **Modelo Semântico** no Lakehouse Gold.

![Lab](/images/semantico.png)

Selecione as tabelas desejadas.

![Lab](/images/semantico01.png)

Modelo criado:

![Lab](/images/semantico02.png)

---
## Criando os Relacionamentos

Arraste os campos para criar os relacionamentos entre Fato e Dimensões.

![Lab](/images/semantico03.png)

Após finalizar:

![Lab](/images/semantico04.png)

---
# 📈 5. Criando Relatórios

## Criando Relatório Manual

Com o modelo semântico aberto, clique em **Relatório em Branco**.

![Lab](/images/report01.png)

Salve como: RPT_Produtos

![Lab](/images/report02.png)

Criando um gráfico para demonstrar produtos:

![Lab](/images/report03.png)

---

## Criando Relatório Automático

Abra o modelo semântico → **Explorar** → **Criar automaticamente um relatório**

![Lab](/images/report04.png)

Resultado final:

![Lab](/images/report05.png)


# 🔁 6. Criando o Pipeline

## 📌 O que é Pipeline?

Um Pipeline no Fabric é o componente responsável por orquestrar a execução de processos de dados.

Ele:

- Não transforma dados  
- Coordena execuções  
- Define dependências  
- Agenda tarefas  

---

## 🎯 O que o Pipeline faz?

- Executa Notebook  
- Executa Dataflow Gen2  
- Copia dados  
- Executa SQL  
- Define dependências  
- Agenda execuções  
- Controla retries  
- Controla paralelismo  

---

## Criando o Pipeline

![Lab](/images/pipeline01.png)

Nome do Pipeline :PL_Produtos
## Adicionando Atividades

Na aba **Atividades**, adicione os três notebooks:

- NB_Get_Data_To_Bronze  
- NB_Bronze_To_Silver  
- NB_Silver_To_Gold  

![Lab](/images/pipeline02.png)

Configure cada notebook informando:

- Workspace  
- Nome do Notebook  

![Lab](/images/pipeline03.png)

Conecte as atividades para execução sequencial.

![Lab](/images/pipeline04.png)

---

## Tratamento de Falhas

O Pipeline permite criar fluxos alternativos para falhas.

---
## Atualizando o Modelo Semântico no Pipeline

Adicione uma atividade para atualizar o Modelo Semântico.

![Lab](/images/pipeline05.png)

Configure a conexão:

![Lab](/images/pipeline06.png)

Crie uma nova conexão:

![Lab](/images/pipeline07.png)

---
## Salvando e Executando

Salve o Pipeline na aba **Início**.

Após salvar:

- Execute manualmente  
- Ou crie um agendamento  

![Lab](/images/pipeline08.png)

Execução com sucesso:

![Lab](/images/pipeline09.png)

---
## Criando Agendamento Automático

Clique em **Agendamento** → **Adicionar Agendamento**

![Lab](/images/pipeline10.png)

Configure:

- Frequência  
- Horário  
- Fuso horário  

---

# 🧠 Conclusão da Arquitetura

Com isso implementamos:

- Arquitetura Medalhão completa  
- Modelo Estrela  
- Modelo Semântico  
- Relatórios  
- Orquestração automatizada 


# 🎓 Encerramento

Este laboratório demonstra como utilizar o Microsoft Fabric para construir uma plataforma moderna de dados, integrando:

- Engenharia de Dados  
- Modelagem Analítica  
- BI  
- Orquestração  

---

> Lakehouse organiza dados.  
> Modelo Semântico organiza significado.  
> Pipeline organiza execução.