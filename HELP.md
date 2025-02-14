# Verificação da Instalação e Configuração do Conjur no OpenShift

## Verificar se o Conjur foi instalado e configurado corretamente

Para verificar visualmente se o Conjur foi instalado e configurado corretamente utilizando a interface gráfica do OpenShift, siga estas etapas:

### Acessar o Console Web do OpenShift

1. Abra seu navegador e acesse o console web do OpenShift.
2. Faça login com suas credenciais de administrador.

### Verificar a Namespace conjur

1. No painel de navegação à esquerda, selecione "Projetos".
2. Procure pelo projeto (namespace) chamado `conjur`.
3. Clique no projeto `conjur` para abrir detalhes específicos.

### Verificar os Pods

1. Dentro do projeto `conjur`, selecione "Workloads" e depois "Pods".
2. Verifique se todos os pods relacionados ao Conjur estão em execução e no estado `Running`.

### Verificar os ConfigMaps e Secrets

1. No mesmo projeto `conjur`, selecione "Workloads" e depois "Config Maps" para verificar os ConfigMaps configurados.
2. Selecione "Secrets" para verificar os Secrets configurados.

### Verificar os Deployments

1. Ainda no projeto `conjur`, selecione "Workloads" e depois "Deployments".
2. Verifique se o deployment do Conjur está corretamente configurado e em execução.

### Verificar os Serviços

1. Dentro do projeto `conjur`, selecione "Networking" e depois "Services".
2. Verifique se o serviço do Conjur está configurado corretamente.

------------

## Acessar a Interface Web do Conjur

Para acessar a interface web do Conjur após a instalação, siga os passos abaixo:

### Obter a URL do Conjur Service

1. No console web do OpenShift, vá até o projeto `conjur`.
2. Selecione "Networking" e depois "Services".
3. Encontre o serviço do Conjur e copie a URL ou o endereço IP associado.

### Acessar a Interface Web do Conjur

1. Abra um navegador web.
2. Digite a URL ou o endereço IP do serviço do Conjur na barra de endereços.
   - A URL deve ser algo como `https://<conjur-service-url>`.

### Login no Conjur

1. Quando a página de login do Conjur aparecer, insira as credenciais do administrador (nome de usuário e senha) que você definiu durante a configuração.
2. Clique em "Login" para acessar o dashboard do Conjur.

Esses passos permitirão que você acesse a interface web do Conjur e gerencie seus segredos diretamente pelo navegador.

----------------

## Acessar o Banco de Dados PostgreSQL do Conjur

O banco de dados PostgreSQL utilizado pelo Conjur é gerenciado internamente pela aplicação e não é destinado para acesso direto pelos usuários. No entanto, é possível acessar o banco de dados para fins de administração e manutenção usando ferramentas e comandos apropriados. Aqui estão algumas maneiras de acessar o banco de dados PostgreSQL do Conjur:

### Acessar o Pod do Conjur

1. Primeiro, você precisa acessar o pod do Conjur onde o banco de dados está em execução. Você pode fazer isso com o seguinte comando:

```sh
oc rsh <nome-do-pod-do-conjur>
```

2. Substitua conjur pelo nome de usuário do banco de dados configurado. Você será solicitado a inserir a senha.

## Executar Comandos SQL

Agora que você está conectado ao banco de dados, pode executar comandos SQL conforme necessário para administração e manutenção. Por exemplo, para listar todas as tabelas:

```sh
\dt
```

Sair do Banco de Dados

Para sair do shell do banco de dados PostgreSQL, você pode usar o comando:
```sh
\q
```