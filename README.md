# Configuração de PostgreSQL com ngrok e Conexão ao Looker Studio

Este guia ajudará você a configurar e expor seu banco de dados PostgreSQL local usando ngrok e conectá-lo ao Looker Studio. Siga os passos abaixo.

## Passo 1: Configurar o PostgreSQL

1. **Editar o arquivo `postgresql.conf`**:
   - Abra o arquivo `postgresql.conf` no diretório do PostgreSQL.
   - Adicione ou edite a linha para permitir conexões de qualquer endereço:
     ```conf
     listen_addresses = '*'
     ```
   - *Inserir imagem 1 aqui*

2. **Editar o arquivo `pg_hba.conf`**:
   - Abra o arquivo `pg_hba.conf` no mesmo diretório.
   - Adicione a seguinte linha para permitir conexões de qualquer IP:
     ```conf
     host    all             all             0.0.0.0/0            md5
     ```
   - *Inserir imagem 2 aqui*

3. **Reiniciar o PostgreSQL**:
   - Reinicie o serviço PostgreSQL para aplicar as mudanças.

## Passo 2: Adicionar `psql` às Variáveis do Sistema

1. **Adicionar Caminho do `psql`**:
   - Abra as Configurações do Sistema, vá para "Variáveis de Ambiente" e edite a variável `Path`.
   - Adicione o caminho do diretório `bin` do PostgreSQL, algo como `C:\Program Files\PostgreSQL\<versão>\bin`.
   - *Inserir imagem 3 aqui*

## Passo 3: Configurar o ngrok

1. **Baixar e Instalar ngrok**:
   - Baixe ngrok em [ngrok.com](https://ngrok.com/), crie uma conta e valide a identidade.
   - Abra o executável ngrok como administrador.
   - *Inserir imagem 4 e 5 aqui*

2. **Autenticar ngrok**:
   - No Prompt de Comando, autentique o ngrok com o token da sua conta:
     ```sh
     ngrok authtoken <seu_token_ngrok>
     ```
   - *Inserir imagem 6 aqui*

3. **Expor a Porta do PostgreSQL**:
   - Execute o seguinte comando para expor a porta 5432 do PostgreSQL:
     ```sh
     ngrok tcp 5432
     ```
   - ngrok fornecerá um endereço público, como `tcp://0.tcp.sa.ngrok.io:XXXXX`.
   - *Inserir imagem 7 aqui*

## Passo 4: Conectar ao PostgreSQL

1. **Usar `psql` para Conectar**:
   - No Prompt de Comando, use o endereço fornecido pelo ngrok para conectar-se ao PostgreSQL:
     ```sh
     psql -h 0.tcp.sa.ngrok.io -p XXXXX -U seu_usuario -d seu_banco_de_dados
     ```
   - Substitua `XXXXX` pelo número da porta fornecido pelo ngrok.

## Passo 5: Conectar ao Looker Studio

1. **Abrir o Looker Studio**.
2. **Criar um Novo Relatório** e selecionar "Adicionar Dados".
3. **Escolher "PostgreSQL"** como conector.
4. **Inserir os Detalhes de Conexão**:
   - **Host**: O endereço público fornecido pelo ngrok (ex: `0.tcp.ngrok.io`).
   - **Porta**: O número da porta fornecido pelo ngrok (ex: `16487`).
   - **Nome do Banco de Dados**: O nome do seu banco de dados PostgreSQL.
   - **Nome de Usuário**: Seu usuário PostgreSQL.
   - **Senha**: A senha do seu usuário PostgreSQL.
   - *Inserir imagem 8 aqui*

Seguindo esses passos, você conseguirá configurar e expor seu banco de dados PostgreSQL local via ngrok e conectá-lo ao Looker Studio para criar seus relatórios e dashboards.
