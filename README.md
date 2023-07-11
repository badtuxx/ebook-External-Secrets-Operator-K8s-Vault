
## O Que Esperar Deste eBook


Bem-vindo ao "Secrets Seguros com Kubernetes, External Secrets Operator e Hashicorp Vault"! Este eBook foi meticulosamente planejado e escrito para profissionais de TI como você, que estão buscando aprofundar suas habilidades e entender como integrar o Kubernetes e o Hashicorp Vault para tornar os secrets do Kubernetes ainda mais seguros. Assumiremos que você já possui familiaridade com o Kubernetes e o Vault, portanto, nosso foco estará na integração dessas duas poderosas ferramentas.
Este eBook está estruturado de uma forma que permite um aprendizado progressivo e interessante, com um toque de humor. Vamos direto ao ponto, com exemplos práticos e analogias do mundo real que tornam a leitura tanto informativa quanto agradável.

Aqui está o que você vai encontrar nos próximos capítulos:

Kubernetes - Uma Visão Rápida: Não vamos passar muito tempo nisso, mas é sempre bom dar uma refrescada na memória.

Vault - Relembrando o Básico: De forma semelhante, vamos rapidamente repassar os conceitos básicos do Vault.

Configurando o Campo de Batalha: Instalando o Vault no Kubernetes: Ação! Aqui, mostraremos como instalar o Vault no Kubernetes, passo a passo.

Conhecendo a Estrela do Show: O External Secrets Operator (ESO): Este capítulo apresentará detalhes sobre o ESO, o protagonista do nosso eBook.

ESO no Palco: Instalando o ESO no Kubernetes: Aprenda a instalar o ESO no Kubernetes, passo a passo.

Preparando o Vault para a Grande Dança: Configuração da Integração com o Vault: Este capítulo aborda os aspectos cruciais da configuração do Vault para a integração.

Entrando em Sintonia: Configurando o Kubernetes para a Integração: Vamos ver os passos necessários para preparar o Kubernetes para essa integração.

Fazendo a Mágica Acontecer: Sincronizando os Secrets: Nesta parte, mergulharemos nos detalhes de como sincronizar os secrets entre o Vault e o Kubernetes.

Colocando Tudo em Jogo: Exemplo de Uso Real: Para encerrar, apresentaremos um exemplo prático da integração, com um toque de realismo e humor.
Embora o assunto seja sério e importante, nosso objetivo é fazer com que essa jornada seja prazerosa e agradável, ajudando você a aprender enquanto se diverte. Vamos lá!

# Kubernetes - Uma Visão Rápida

Mesmo que já estejamos confortáveis com o conceito do Kubernetes, é sempre bom revisitar algumas noções básicas e verificar se estamos todos na mesma página.

## O Que é Kubernetes?

Kubernetes, também conhecido como K8s, é uma plataforma open-source poderosa e altamente flexível para gerenciar cargas de trabalho e serviços em contêiner. Ela automatiza a implantação, o dimensionamento e a gestão de aplicações em contêineres.

## Núcleo do Kubernetes

A essência do Kubernetes está na orquestração de contêineres. Com sua ajuda, você pode gerenciar centenas, até mesmo milhares, de contêineres de maneira eficiente e eficaz. Ele agrupa contêineres que formam uma aplicação em unidades lógicas, tornando o gerenciamento e a descoberta mais fáceis.

## Comandos Básicos do Kubernetes

Agora, vamos nos aprofundar um pouco mais e relembrar alguns comandos básicos do Kubernetes. Sabemos que na vida real, é aí que a ação realmente acontece!

**Obter Informações sobre o Cluster**

```bash
kubectl cluster-info
```

Este comando fornecerá informações básicas sobre o seu cluster, como a URL do servidor mestre e os serviços que estão em execução.

**Listar Todos os Pods**

```bash
kubectl get pods
```

Este comando exibirá todos os pods que estão em execução no seu cluster.

**Iniciar um Pod**

```bash
kubectl run my-pod --image=my-image
```

Este comando iniciará um pod chamado "my-pod" com a imagem "my-image".

**Deletar um Pod**

```bash
kubectl delete pod my-pod
```

Este comando deletará o pod chamado "my-pod".

Lembre-se de que esses são apenas os comandos mais básicos. À medida que avançamos em direção à integração do Kubernetes com o Vault, veremos comandos muito mais complexos e interessantes.

Este breve resumo deve ter ajudado a refrescar sua memória sobre o Kubernetes. Agora estamos prontos para seguir em frente e explorar o próximo tema: o HashiCorp Vault!


# Os Segredos do Kubernetes

O Kubernetes tem um recurso integrado para gerenciar informações sensíveis chamado "Secrets". Os Secrets permitem armazenar e gerenciar informações sensíveis, como senhas, tokens OAuth e chaves ssh.

## Como Funcionam os Secrets no Kubernetes

Os Secrets são criados diretamente pelo Kubernetes ou usando um gerenciador de configuração e podem ser montados em pods como arquivos para serem usados por aplicativos em contêineres. Eles também podem ser usados pelo sistema para realizar ações em nome de um pod.

Aqui está um exemplo de comando para criar um Secret:

```bash
kubectl create secret generic my-secret --from-literal=password=my-password
```

Esse comando cria um Secret chamado "my-secret" com a senha "my-password".

## O Problema com os Secrets

Apesar dos Secrets serem úteis, eles têm algumas limitações significativas. Em primeiro lugar, os Secrets não são criptografados por padrão. Eles são apenas codificados em base64, o que não é uma forma segura de armazenar informações sensíveis. Além disso, os Secrets são armazenados no etcd, o banco de dados do Kubernetes, que pode ser um alvo atraente para atacantes.

Outro problema é a gestão dos Secrets. Em grandes organizações com muitos Secrets, pode ser desafiador manter o controle de todos eles, garantir que estão sendo usados corretamente e que estão sendo atualizados conforme necessário.

## A Solução

É aqui que a nossa estrela, o External Secrets Operator (ESO), junto com o HashiCorp Vault, entra em jogo. Ao longo deste eBook, vamos explorar como podemos usar o ESO para sincronizar os Secrets entre o Kubernetes e o Vault, fornecendo uma maneira segura e eficiente de gerenciar nossos Secrets. Além disso, aprenderemos como podemos automatizar esse processo para garantir que nossos Secrets estejam sempre atualizados e seguros. 

Portanto, se você está cansado de lidar com Secrets desorganizados e quer saber como torná-los mais seguros e gerenciáveis, continue lendo, pois temos uma jornada emocionante pela frente!

# Vault - Relembrando o Básico

Assim como fizemos com o Kubernetes, vamos rever rapidamente o que é o Vault, qual é sua função e por que ele é tão crucial para nossa jornada.

## O Que é o Vault?

HashiCorp Vault é uma ferramenta para gerenciar segredos de maneira segura. Ele permite que você armazene e controle o acesso a tokens, senhas, certificados, chaves de criptografia e outras informações sensíveis. No nosso contexto, o Vault se torna uma solução poderosa para superar os problemas inerentes à maneira como o Kubernetes lida com os Secrets.

## Por que Usar o Vault?

Com o Vault, você pode centralizar a gestão de segredos, reduzindo a superfície de ataque e minimizando o risco de vazamento de dados. O Vault também oferece controle detalhado de políticas de acesso, permitindo determinar quem pode acessar o que, quando e onde.

## Comandos Básicos do Vault

O Vault pode ser um pouco complexo para os novatos, mas se você já trabalhou com ele, os comandos básicos são relativamente simples.

**Instalando o Hashicorp Vault**

```bash
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update && sudo apt install vault
```

**Iniciando o Vault em Modo Dev**

```bash
vault server -dev
```

Este comando inicia o Vault em modo de desenvolvimento, que é útil para fins de aprendizado e experimentação.

**Configurando o Vault CLI para apontar para o nosso Vault**

```bash
export VAULT_ADDR='http://127.0.0.1:8200'
```

Isso define a variável de ambiente `VAULT_ADDR`, apontando para o endereço do servidor Vault.

**Escrevendo Secrets**

```bash
vault kv put secret/my-secret password=my-password
```

Este comando escreve um segredo chamado "my-secret" com a senha "my-password".

**Lendo Secrets**

```bash
vault kv get secret/my-secret
```

Este comando lê o segredo chamado "my-secret".

## O Vault no Contexto do Kubernetes

Agora que você se lembrou do básico do Vault, a próxima etapa é entender como ele pode trabalhar em conjunto com o Kubernetes e o ESO para aprimorar a gestão de segredos. Estamos prestes a embarcar em uma jornada emocionante que envolve a instalação do Vault no Kubernetes e a configuração da integração do Vault, então, prepare-se!



# Instalando e Configurando o Vault no Kubernetes

Vamos agora mergulhar na parte prática. Vamos configurar o Vault no Kubernetes, passo a passo, utilizando o Helm. No final deste processo, teremos o Vault instalado, configurado e pronto para o uso.

## Pré-requisitos

Antes de começar, certifique-se de que você tem o seguinte:

1. Uma instância do Kubernetes em execução.
2. O Helm instalado em sua máquina local ou no seu cluster.
## Instalando e Configurando o Vault com Helm

Aqui estão os passos para instalar e configurar o Vault usando o Helm:

**1. Adicione o repositório HashiCorp ao Helm**

```bash
helm repo add hashicorp https://helm.releases.hashicorp.com
```

Este comando adiciona o repositório Helm da HashiCorp à nossa configuração do Helm.

**2. Instale o Vault usando Helm**

```bash
helm install vault hashicorp/vault
```

Este comando instala o Vault no cluster Kubernetes.

**3. Instalando o CLI do Vault**

```bash
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update && sudo apt install vault
```

**Configurando o Vault CLI para apontar para o nosso Vault**

```bash
kubectl get svc vault
export VAULT_ADDR='http://<IP_SERVICE>:8200'
vault status
```

Este comando cria uma variável de ambiente que irá permitir que interajamos diretamente com o Vault que instalamos no Kubernetes via Helm.

**4. Inicialize e desbloqueie o Vault**

```bash
vault operator init
vault operator unseal
vault login
```

Estes comandos inicializam o Vault, removem o selo e fazem login.

**5. Habilite o armazenamento de segredos e adicione alguns segredos para teste**

```bash
vault secrets enable -path=linuxtips kv
vault kv put linuxtips/senha palavra1=giropops palavra2=strigus
```
Estes comandos habilitam o armazenamento de segredos e adicionam um segredo de exemplo ao caminho "linuxtips/senha".

**6. Crie uma política no Vault**

```bash
vim minha-policy.hcl
```

Adicione esse conteúdo:

```hcl
path "linuxtips/senha" { 
  capabilities = ["read"]
} 
```

```bash
vault policy write minha-policy minha-policy.hcl
```

Este comando cria uma política chamada "minha-policy" que concede permissões de leitura no caminho "linuxtips/senha".


**7. Crie um token com a política que você acabou de definir**

```bash
vault token create -policy="minha-policy"
```

Este comando cria um token vinculado à política "minha-policy".

E é isso! Agora você tem o Vault instalado e configurado no seu cluster Kubernetes. O próximo passo é instalar e configurar o External Secrets Operator, que é o foco principal deste eBook.


# External Secrets Operator (ESO) - O Astro Desse Show

É agora que a nossa estrela, o External Secrets Operator (ESO), entra em cena. Então, vamos nos familiarizar um pouco com ele antes de prosseguir.

## Uma Breve Apresentação do ESO

External Secrets Operator é um maestro para os segredos do Kubernetes, capaz de trabalhar em perfeita harmonia com uma grande variedade de sistemas de gerenciamento de segredos externos. Isso inclui, mas não se limita a, gigantes como AWS Secrets Manager, HashiCorp Vault, Google Secrets Manager, Azure Key Vault e IBM Cloud Secrets Manager.

O papel do ESO é buscar informações dessas APIs externas e trazer para o palco do Kubernetes, transformando-as em Kubernetes Secrets prontos para uso.

## O Papel de Destaque do ESO

A grande missão do ESO é sincronizar segredos de APIs externas para o ambiente do Kubernetes. Para tanto, ele se utiliza de três recursos de API personalizados: ExternalSecret, SecretStore e ClusterSecretStore. Estes recursos criam uma ponte entre o Kubernetes e as APIs externas, permitindo que os segredos sejam gerenciados e utilizados de maneira amigável e eficiente.

Para simplificar, o ESO é o nosso agente secreto, trazendo os segredos de várias fontes externas para os aplicativos do Kubernetes, garantindo que eles sejam entregues de forma segura e controlada.

# Conceitos-Chave do External Secrets Operator

Vamos explorar alguns conceitos fundamentais para o nosso trabalho com o External Secrets Operator (ESO).

## SecretStore

O SecretStore é um recurso que separa as preocupações de autenticação/acesso e os segredos e configurações necessários para as cargas de trabalho. Este recurso é baseado em namespaces.

Imagine o SecretStore como um gerente de segredos que conhece a forma como acessar os dados. Ele contém referências a segredos que mantêm as credenciais para acessar a API externa.

Aqui está um exemplo simplificado de como o SecretStore é definido:

```yaml
apiVersion: external-secrets.io/v1beta1
kind: SecretStore
metadata:
  name: secretstore-sample
spec:
  provider:
    aws:
      service: SecretsManager
      region: us-east-1
      auth:
        secretRef:
          accessKeyIDSecretRef:
            name: awssm-secret
            key: access-key
          secretAccessKeySecretRef:
            name: awssm-secret
            key: secret-access-key
```

## ExternalSecret

Um ExternalSecret declara quais dados buscar e tem uma referência ao SecretStore, que sabe como acessar esses dados. O controlador usa esse ExternalSecret como um plano para criar segredos.

Pense em um ExternalSecret como um pedido feito ao gerente de segredos (SecretStore) para buscar um segredo específico. A configuração do ExternalSecret define o que buscar, onde buscar e como formatar o segredo.

Aqui está um exemplo simplificado de como o ExternalSecret é definido:

```yaml
apiVersion: external-secrets.io/v1beta1
kind: ExternalSecret
metadata:
  name: example
spec:
  refreshInterval: 1h
  secretStoreRef:
    name: secretstore-sample
    kind: SecretStore
  target:
    name: secret-to-be-created
    creationPolicy: Owner
  data:
  - secretKey: secret-key-to-be-managed
    remoteRef:
      key: provider-key
      version: provider-key-version
      property: provider-key-property
  dataFrom:
  - extract:
      key: remote-key-in-the-provider
```

## ClusterSecretStore

O ClusterSecretStore é um SecretStore global, que pode ser referenciado por todos os namespaces. Você pode usá-lo para fornecer um gateway central para seu provedor de segredos. É como um SecretStore, mas com alcance em todo o cluster, ao invés de apenas um namespace.

## Controle de Acesso e Segurança

O ESO é um operador poderoso com acesso elevado. Ele cria/lê/atualiza segredos em todos os namespaces e tem acesso a segredos armazenados em algumas APIs externas. Portanto, é vital garantir que o ESO tenha apenas os privilégios mínimos necessários e que o SecretStore/ClusterSecretStore seja projetado com cuidado.

Além disso, considere a utilização do sistema de controle de admissão do Kubernetes (como OPA ou Kyverno) para um controle de acesso mais refinado.

Agora que temos um bom entendimento dos conceitos-chave, vamos prosseguir para a instalação do ESO no Kubernetes.




# Configurando o External Secrets Operator

Vamos dar uma olhada em como instalar e configurar o External Secrets Operator no Kubernetes.

## Adicionando o Repositório External Secrets ao Helm

Antes de instalar o ESO, precisamos adicionar o repositório External Secrets ao Helm. Faça isso com os seguintes comandos:

```bash
helm repo add external-secrets https://charts.external-secrets.io
```

## Instalando o External Secrets Operator

Após a adição do repositório, você pode instalar o ESO com o comando abaixo:

```bash
helm install external-secrets external-secrets/external-secrets -n external-secrets --create-namespace --set installCRDs=true
```

## Verificando a Instalação do ESO

Para verificar se o ESO foi instalado corretamente, você pode executar o seguinte comando:

```bash
kubectl get all -n external-secrets
```

## Criando um Segredo no Kubernetes

Agora, precisamos criar um segredo no Kubernetes que contém o token do Vault. Faça isso com o seguinte comando:

```bash
kubectl create secret generic vault-policy-token --from-literal=token=O_TOKEN_DA_POLICY_QUE_CRIAMOS
```

Lembre-se de substituir `SEU_TOKEN_DO_VAULT` pelo token real que você obteve do Vault.

Para verificar se o segredo foi criado corretamente, você pode executar o seguinte comando:

```bash
kubectl get secrets
```

## Configurando o ClusterSecretStore

O próximo passo é configurar o ClusterSecretStore, que é o recurso que fornecerá um gateway central para seu provedor de segredos. Para fazer isso, você precisa criar um arquivo chamado `cluster-store.yaml` com o seguinte conteúdo:

```yaml
apiVersion: external-secrets.io/v1beta1
kind: ClusterSecretStore #Kubernetes resource type
metadata:
  name: vault-backend #resource name
spec:
  provider:
    vault: #specifies vault as the provider
      server: "http://IP_DO_VAULT_SVC:8200" #the address of your vault instance
      path: "linuxtips" #path for accessing the secrets
      version: "v1" #Vault API version
      auth:
        tokenSecretRef:
          name: "vault-policy-token" #Use a secret called vault-token
          key: "token" #Use this key to access the vault token
```

Para aplicar essa configuração ao Kubernetes, use o seguinte comando:

```bash
kubectl apply -f cluster-store.yaml
```

## Criando um ExternalSecret

Finalmente, precisamos criar um ExternalSecret que especifica quais dados buscar do provedor de segredos. Para fazer isso, crie um arquivo chamado `ex-secrets.yaml` com o seguinte conteúdo:

```yaml
apiVersion: external-secrets.io/v1beta1
kind: ExternalSecret
metadata:
  name: external-secret
spec:
  refreshInterval: "10s"
  secretStoreRef:
    name: vault-backend
    kind: ClusterSecretStore
  target:
    name: linuxtips-senhas
    creationPolicy: Owner
  data:
    - secretKey: palavra1
      remoteRef:
        key: linuxtips/senha
        property: palavra1
    - secretKey: palavra2
      remoteRef:
        key: linuxtips/senha
        property: palavra2
```

Para aplicar essa configuração ao Kubernetes, use o seguinte comando:

```bash
kubectl apply -f ex-secrets.yaml
```

Para verificar a criação do ExternalSecret, você pode executar o seguinte comando:

```bash
kubectl get externalsecret
```

E aí está! Você instalou e configurou com sucesso o External Secrets Operator no Kubernetes. Lembre-se, este é apenas um exemplo de como usar o ESO para integrar o Vault com o Kubernetes, mas os mesmos princípios se aplicam a outros provedores de segredos.

