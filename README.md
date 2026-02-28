# 🚀 Microsoft Azure Fabric

![Microsoft Fabric](https://img.shields.io/badge/Microsoft-Fabric-blue)
![Lakehouse](https://img.shields.io/badge/Architecture-Lakehouse-green)
![Delta](https://img.shields.io/badge/Format-Delta%20Lake-orange)
![Medallion](https://img.shields.io/badge/Pattern-Medallion-purple)

---

# 📌 Objetivo do Curso

Este curso tem como objetivo construir uma arquitetura moderna de dados utilizando **Microsoft Fabric**, aplicando:

- Ingestão de Dados
- Lakehouse com OneLake
- Arquitetura Medalhão (Bronze / Silver / Gold)
- Delta Lake
- Upsert (MERGE)
- Modelagem estrela (Fato e Dimensão)
- Consultas analíticas via SQL Endpoint

---

# 🆓 Como Habilitar o Microsoft Fabric Trial

Para executar os laboratórios deste curso, você precisará ativar o **Microsoft Fabric Trial Capacity**.

## ✅ Pré-requisitos

- Conta Microsoft corporativa ou educacional
- Acesso ao portal Fabric
- Permissão para criar Workspaces

## Passo a Passo

Acesse ao site da Azure https://portal.azure.com/

## Entra no Microsoft Entra ID para criar uma conta

![Lab](/images/1.png)


## Criando seu usuário
![Lab](/images/2.png)

![Lab](/images/3.png)

> [!IMPORTANT]
> Guarde as informações `User Principal name` e `Password`

## Atribuindo a permissão para acessar o Fabric
![Lab](/images/4.png)


![Lab](/images/5.png)


## Será que deu certo ?
![Lab](/images/6.png)

Acesse ao site do Fabic https://app.fabric.microsoft/

Alguns passo para iniciar o Fabric

![Lab](/images/8.png)

![Lab](/images/9.png)

![Lab](/images/10.png)


## Validando conta trail do Azure Fabric
![Lab](/images/11.png)

## Mude a visão para o Fabric
![Lab](/images/12.png)


-------
# 🆓 Como Habilitar o Microsoft Fabric Trial


# Criar um lakehouse

## Subir nosso primeiro arquivo

## shortcut fabric

## trabalhar com criação de tabelas

## Otimizar tabelas

O Spark é uma estrutura de processamento paralelo, com dados armazenados em um ou mais nós de trabalho. Além disso, os arquivos Parquet são imutáveis, com novos arquivos gravados para cada atualização ou exclusão. Esse processo pode resultar no armazenamento de dados do Spark em um grande número de arquivos pequenos, conhecidos como o pequeno problema de arquivo. Isso significa que as consultas em grandes quantidades de dados podem ser executadas lentamente ou até mesmo falhar na conclusão.

### Função OptimizeWrite


<<image: otimizador-spark01>>

No Microsoft Fabric, OptimizeWrite está habilitado por padrão.


<<IMAGE>otimizador-spark02.png

### Função v-ORDER

V-Order vem habilitado por padrão no Microsoft Fabric e é aplicado enquanto os dados são gravados. Ele gera uma pequena sobrecarga de cerca de 15%, tornando as gravações um pouco mais lentas. 

O Spark e outros mecanismos não utilizam a tecnologia Verti-Scan, mas ainda assim se beneficiam da otimização V-Order, com leituras até 10% mais rápidas, chegando a 50% em alguns casos.

1 No Lakehouse Explorer, selecione o... menu ao lado de um nome de tabela e selecione Manutenção.
2 Selecione executar o comando OTIMIZAR.
3 Você pode opcionalmente selecionar Aplicar V-order para maximizar as velocidades de leitura no Fabric.
4 Selecione Executar agora.

<IMAGE:table-maintenance-v-order.png>

### Função Vácuo

O comando VACUUM permite remover arquivos de dados antigos.

<<IMAGEM>how-vacuum-works.png>

Sempre que uma atualização ou exclusão é feita, um novo arquivo Parquet é criado e uma entrada é registrada no log de transações. Arquivos Parquet antigos são mantidos para possibilitar a viagem no tempo, o que significa que os arquivos Parquet se acumulam com o tempo.


### Partições


## Stream
Ao usar uma tabela Delta como uma fonte de streaming, apenas operações de acréscimo podem ser incluídas no stream. As modificações de dados podem causar erro, a menos que você especifique as opções ignoreChanges ou ignoreDeletes.



# Eventhouse


Quando você cria um Eventhouse, um banco de dados KQL padrão é criado automaticamente com o mesmo nome. Um Eventhouse contém um ou mais bancos de dados KQL, onde você pode criar tabelas, procedimentos armazenados, exibições materializadas, funções, fluxos de dados e atalhos para gerenciar seus dados.

## Linguagem KQL

O KQL usa uma abordagem de pipeline, em que os dados fluem de uma operação para a outra usando o caractere de barra vertical (|). Pense nele como um funil: você começa com uma tabela de dados inteira e cada operador filtra, reorganiza ou resume os dados antes de passá-los para a próxima etapa. A ordem dos operadores é importante porque cada etapa se baseia nos resultados da etapa anterior.


TaxiTrips
| where fare_amount > 20
| project trip_id, pickup_datetime, fare_amount
| take 10

