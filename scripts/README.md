# =� Scripts do Backend

Esta pasta cont�m scripts utilit�rios para o backend da Casa+.

## =� Scripts Dispon�veis

### =� **Setup e Configura��o**

#### `setup-db.js`

Cria o banco de dados e todas as tabelas necess�rias.

```bash
# Executar via npm
npm run setup-db

# Ou diretamente
node scripts/setup-db.js
```

**Funcionalidades:**
-  Cria banco de dados `casamais_db`
-  Cria todas as tabelas com relacionamentos
-  Configura �ndices e constraints
-  Verifica conex�o com MySQL

### =� **Popula��o de Dados**

#### `populate-db.js`

Popula o banco com dados de exemplo originais, e faz a migra��o dos dados existentes de doa��es para doadores

```bash
# Executar via npm
npm run populate-db

# Ou diretamente
node scripts/populate-db.js
```

**Funcionalidades:**

-  Dados de assistidas, medicamentos, doa��es
-  Estrutura original do sistema
-  Valida��o de tabelas existentes

#### `populate-doadores.js`

Popula o banco com doadores que possuem CPF/CNPJ v�lidos e endere�os completos.

```bash
# Executar via npm
npm run populate-doadores

# Ou diretamente
node scripts/populate-doadores.js
```

**Funcionalidades:**

-  Gera 10 doadores PF com CPFs v�lidos
-  Gera 10 doadores PJ com CNPJs v�lidos
-  Endere�os brasileiros completos
-  Limpa dados existentes antes de popular
-  Cria doa��es associadas aos doadores

### = **Valida��o**

#### `validar-documentos.js`

Valida todos os CPFs e CNPJs no banco de dados.

```bash
# Executar via npm
npm run validate-docs

# Ou diretamente
node scripts/validar-documentos.js
```

**Funcionalidades:**

-  Valida CPFs usando algoritmo oficial
-  Valida CNPJs usando algoritmo oficial
-  Mostra estat�sticas de valida��o
-  Lista exemplos de documentos v�lidos

### >� **Testes de API**

#### `test_doadores_endpoints.sh`

Testa todos os endpoints da API de doadores.

```bash
# Executar via npm
npm run test:doadores

# Ou diretamente
bash scripts/test_doadores_endpoints.sh
```

**Testes inclusos:**

-  Listar doadores
-  Criar doador PF/PJ
-  Buscar por ID
-  Filtros (tipo, busca)
-  Atualizar doador
-  Hist�rico de doa��es
-  Valida��es de erro
-  Desativar doador

#### `test_doacoes_endpoints.sh`

Testa todos os endpoints da API de doa��es.

```bash
# Executar via npm
npm run test:doacoes

# Ou diretamente
bash scripts/test_doacoes_endpoints.sh
```

**Testes inclusos:**

-  Listar doa��es
-  Criar com doador existente
-  Criar com novo doador (compatibilidade)
-  Buscar por ID
-  Filtros (per�odo, tipo, doador)
-  Atualizar doa��o
-  Estat�sticas
-  Valida��es de erro
-  Excluir doa��o

## =' Pr�-requisitos

Para executar os scripts:

1. **Servidor rodando**: `npm run dev`
2. **Banco configurado**: `npm run setup-db`
3. **Depend�ncias instaladas**: `npm install`

## =� Sa�da dos Scripts

### Popula��o de Doadores

```
=� Iniciando popula��o de doadores com dados v�lidos...

 Conectado ao banco de dados
= Limpando doadores existentes...
= Inserindo doadores PF com CPFs v�lidos...
= Inserindo doadores PJ com CNPJs v�lidos...
= Criando doa��es para os doadores...

=� Dados inseridos com sucesso:
   - Doadores: 20
   - Doa��es: 20
   - Total arrecadado: R$ 10125.00

= Exemplos de CPFs gerados:
   Maria Silva Santos: 29415498110 
   Jo�o Pedro Oliveira: 29227197907 
   Ana Beatriz Costa: 35674996610 

 Popula��o de doadores conclu�da com sucesso!
```

### Valida��o de Documentos

```
= Validando documentos gerados...

=� Resultado da valida��o:
    CPFs v�lidos: 10
   L CPFs inv�lidos: 0
    CNPJs v�lidos: 10
   L CNPJs inv�lidos: 0

<� Exemplos de endere�os gerados:
   Maria Silva Santos: Alameda Bela Vista, 1172, Santo Andr�/PI - CEP: 34019924
   Jo�o Pedro Oliveira: Pra�a Paulista, 3102, Belo Horizonte/SC - CEP: 52569127
```

### Testes de API

```
>� TESTANDO ENDPOINTS DE DOADORES
==================================

1�  GET - Listar todos os doadores
Status: 200 

2�  POST - Criar doador Pessoa F�sica
Status: 201 

...

 TODOS OS TESTES CONCLU�DOS!
```

## =� Personaliza��o

### Adicionando Novos Scripts

1. Crie o arquivo na pasta `scripts/`
2. Adicione permiss�o de execu��o: `chmod +x scripts/nome_script.sh`
3. Adicione ao `package.json`:
   ```json
   "scripts": {
     "meu-script": "node scripts/meu-script.js"
   }
   ```

### Modificando Popula��o

Para alterar os dados gerados, edite:

- `populate-doadores.js` - Nomes, endere�os, valores
- Fun��es `gerarCPFValido()` e `gerarCNPJValido()`
- Arrays de dados fake (cidades, estados, etc.)

## = Resolu��o de Problemas

### Erro de Conex�o

```bash
L Erro: Access denied for user 'root'@'localhost'
```

**Solu��o**: Verifique as credenciais no `.env`

### Erro de Foreign Key

```bash
L Erro: Cannot add or update a child row: a foreign key constraint fails
```

**Solu��o**: Execute o script de limpeza antes de popular

### Scripts n�o Executam

```bash
L Permission denied
```

**Solu��o**: `chmod +x scripts/*.sh`

## =� Documenta��o Relacionada

- **[../docs/CURL_COMMANDS.md](../docs/CURL_COMMANDS.md)** - Comandos curl manuais
- **[../docs/DOCUMENTOS_VALIDOS.md](../docs/DOCUMENTOS_VALIDOS.md)** - Valida��o CPF/CNPJ
- **[../README.md](../README.md)** - Documenta��o principal

---

**Scripts organizados para melhor produtividade! =�**