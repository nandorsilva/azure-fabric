# 🚀 Microsoft Fabric – Curso Prático de Arquitetura Lakehouse

![Microsoft Fabric](https://img.shields.io/badge/Microsoft-Fabric-blue)
![Lakehouse](https://img.shields.io/badge/Architecture-Lakehouse-green)
![Delta](https://img.shields.io/badge/Format-Delta%20Lake-orange)
![Medallion](https://img.shields.io/badge/Pattern-Medallion-purple)

---

# 📌 Objetivo do Curso

Este curso tem como objetivo construir uma **arquitetura moderna de dados utilizando Microsoft Fabric**, aplicando conceitos e práticas reais de Engenharia de Dados.

Durante o treinamento, o aluno irá implementar:

- ✅ Ingestão de Dados
- ✅ Lakehouse com OneLake
- ✅ Arquitetura Medalhão (Bronze / Silver / Gold)
- ✅ Delta Lake
- ✅ Upsert com MERGE
- ✅ Modelagem Estrela (Fato e Dimensão)
- ✅ Consultas analíticas via SQL Endpoint
- ✅ Otimização de tabelas
- ✅ Introdução ao Eventhouse e KQL

---

# 🧱 Arquitetura do Curso

A arquitetura implementada no laboratório segue o padrão **Lakehouse + Medalhão**:


Todos os dados são armazenados no **OneLake**, utilizando tabelas no formato **Delta Lake**.

---

# 🆓 Como Habilitar o Microsoft Fabric Trial

Para executar os laboratórios deste curso, é necessário ativar o **Microsoft Fabric Trial Capacity**.

---

## ✅ Pré-requisitos

- Conta Microsoft corporativa ou educacional
- Permissão para criar Workspaces

---

## 🔹 Passo 1 – Acesse o Portal Azure

Acesse:

https://portal.azure.com

---

## 🔹 Passo 2 – Criar usuário no Microsoft Entra ID

Entre no **Microsoft Entra ID** para criar seu usuário de acesso ao ambiente.

![Lab](/images/1.png)

### Criando o usuário

![Lab](/images/2.png)

![Lab](/images/3.png)

> ⚠️ **Importante**  
> Guarde as informações de:
> - `User Principal Name`
> - `Password`

---

## 🔹 Passo 3 – Atribuir Permissão ao Fabric

Conceda a permissão necessária para acesso ao Microsoft Fabric.

![Lab](/images/4.png)

![Lab](/images/5.png)

---

## 🔹 Passo 4 – Validar se o acesso foi concedido

![Lab](/images/6.png)

---

## 🔹 Passo 5 – Acessar o Fabric

Acesse:

https://app.fabric.microsoft.com

Primeiros passos dentro do Fabric:

![Lab](/images/8.png)

![Lab](/images/9.png)

![Lab](/images/10.png)

---

## 🔹 Validando o Trial Capacity

![Lab](/images/11.png)

---

## 🔹 Alterando a Visão para Fabric

![Lab](/images/12.png)

---

## 🔹 Criando nosso Primeiro WorkSpace
![Lab](/images/woskspace.png)


![Lab](/images/woskspace02.png)

Workspace Ativo
![Lab](/images/woskspace03.png)



# 🏗️ Trabalhando com Lakehouse

## 📌 Criar um Lakehouse


Criando Lakehouse

![Lab](/images/lakehouse01.png)

Informe nome `LH_Bronze`

![Lab](/images/lakehouse02.png)

Observe o Gerenciador do LakeHouse
![Lab](/images/lakehouse03.png)

> ⚠️ **Importante**  
> A pasta dbo representa o schema padrão (default schema) das tabelas no Lakehouse quando acessadas via SQL Endpoint.
> Ela não é um banco relacional tradicional, mas sim uma organização lógica baseada em schema.

---

## 📂 Subir o Primeiro Arquivo

- Upload manual
- Ingestão via Notebook
- Criação de tabela Delta

![Lab](/images/lakehouse04.png)

Arquivo Carregado

![Lab](/images/lakehouse05.png)


### Transformando nosso arquivo para o formato Parquet

Na opção de "..." do nosso arquivo.

![Lab](/images/lakehouse06.png)

### Carregando o arquivo, pode deixar o mesno nome do arquivo

Esquema : dbo
Nome da tabela:20260201_produto

![Lab](/images/lakehouse07.png)

### Se deu tudo certo???

![Lab](/images/lakehouse08.png)

### Muda a exibição para arquivo

![Lab](/images/lakehouse09.png)
---


## 🔗 Criar Shortcut no Fabric

Os **Shortcuts** permitem apontar para:

- Azure Data Lake Storage
- Amazon S3
- Outro Lakehouse
- Banco KQL (Eventhouse)

Sem necessidade de copiar os dados fisicamente.

### Mas antes um lá no portal da azure, criar um Storage Account.

![Lab](/images/storage01.png)

![Lab](/images/storage02.png)

### Busca o endpoint do Data Lake Storage

Data Lake Storage: https://storagefabricdemo001.dfs.core.windows.net/

![Lab](/images/storage03.png)

Crie o containers ´files`e suba o arquivo `csv`


### Configurando o acesso ao usuário conectado do fabric

![Lab](/images/storage04.png)

Sigua as etapas para `Role`e `Member`

1. Procure em Role `Storage Blob Data Contributor`
![Lab](/images/storage05.png)

2. Em menber o usuário logado no fabric
![Lab](/images/storage06.png)

Conclua o processo, e volte para o Fabric, adicionando um novo Shortcuts/Atalho

![Lab](/images/Shortcut01.png)

Selecione a fonte Azure Data Lake Storage Gen2 e crie uma nova conexão.
![Lab](/images/Shortcut02.png)

Criando a conexão
![Lab](/images/Shortcut03.png)

Selecionando o container  `files` criando anteriormente
![Lab](/images/Shortcut04.png)
---

# 📊 Trabalhando com Tabelas Delta

## Vamos criar nosso primeiro Notebook

Nome: Tabela_Delta
![Lab](/images/notebook01.png)

Inseri a fonte de dados Lakehouse `LH_Bronze`

![Lab](/images/notebook02.png)

Copiando o endereço ABFS
![Lab](/images/notebook03.png)

### Execute o notebook `Tabela_Delta` e tenha o resultado abaixo:

![Lab](/images/notebook04.png)




---

# ⚡ Otimização de Tabelas no Fabric

O Spark é um mecanismo de processamento distribuído.  
Arquivos Parquet são imutáveis — cada update/delete gera novos arquivos.

Isso pode gerar o problema conhecido como:

> **Small Files Problem**

Quando há muitos arquivos pequenos, consultas podem ficar lentas.

![Lab](/images/otimizador-spark02.png)


---

## 🔹 Optimize Write

No Microsoft Fabric, o **OptimizeWrite** já vem habilitado por padrão.

Ele:
- Reduz geração de arquivos pequenos
- Melhora organização de escrita



---

## 🔹 V-Order

O **V-Order** é uma tecnologia de otimização física aplicada no momento da gravação.

✔ Habilitado por padrão no Fabric  
✔ Pode melhorar leitura em até 50%  
✔ Pode gerar ~15% de overhead na escrita  

### Executando manualmente:

1. No Lakehouse Explorer → `...` ao lado da tabela  
2. Selecionar **Manutenção**
3. Executar comando **OTIMIZAR**
4. (Opcional) Aplicar V-order
5. Executar agora

![Lab](/images/otimizador-spark03.png)

---

## 🔹 VACUUM

O comando `VACUUM` remove arquivos antigos não utilizados.

Sempre que ocorre:
- UPDATE
- DELETE
- MERGE

Um novo arquivo Parquet é criado e o antigo permanece para suportar:

> ⏳ **Time Travel**

Com o tempo, esses arquivos se acumulam.

O `VACUUM` limpa esses arquivos antigos.

---

## 🔹 Particionamento

Partições ajudam a:

- Reduzir tempo de leitura
- Melhorar performance de filtros
- Organizar grandes volumes de dados

Exemplo:

```python
df.write \
  .format("delta") \
  .partitionBy("ano", "mes") \
  .saveAsTable("vendas")