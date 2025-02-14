# Esse repo é apenas uma POC para estudo do conjur, não é um playbook com boas praticas para produção.

# Guia de Acesso ao Conjur e OpenShift

## Para rodar o playbook é necessário que você tenha o ansible instalado, caso não tenha pode executa-lo usando a linha abaixo:
> antes de executar a instalação recomendo a a leitura da [documentação oficial](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) 
```bash
sudo apt update && sudo apt install ansible unzip git -y
```

## Para executar o playbook do openshift utilize a linha de comando abaixo:
```sh
ansible-playbook -i hosts instala_openshift.yml --extra-vars "sudo_password=SENHA_ROOT become_user=ROOT_USER" --ask-become-pass
```

## Acesso ao Console do OpenShift

Para abrir o console do OpenShift, siga os passos abaixo:

1. **Obtenha as Credenciais de Acesso**:
   - Após iniciar o cluster com o comando `crc start`, você deve receber as credenciais de acesso, que geralmente incluem o URL do console web, o usuário (usualmente `kubeadmin`) e a senha.

2. **Acesse o Console Web do OpenShift**:
   - Abra um navegador web.
   - Digite o URL do console web recebido durante a instalação. Normalmente, o URL se parece com `https://<crc-ip>:<porta>`, onde `<crc-ip>` é o IP do seu cluster CRC.

3. **Faça Login no Console Web**:
   - No prompt de login, insira o usuário `kubeadmin` e a senha que foi gerada durante o comando `crc start`.

4. **Navegue no Console**:
   - Após fazer login, você terá acesso à interface web do OpenShift, onde poderá gerenciar projetos, implantações, pods, serviços e muito mais.

Se você precisar recuperar as credenciais novamente, pode usar o comando:

```sh
crc console --credentials
```

## Para executar o playbook do conjur utilize a linha de comando abaixo:
```sh
ansible-playbook -i hosts conjur_helm.yml --extra-vars "sudo_password=SENHA_ROOT become_user=ROOT_USER" --ask-become-pass
```

## Acesso ao Conjur

Após rodar o playbook Ansible, siga os passos abaixo para acessar o Conjur:

1. **Obtenha o URL do Serviço do Conjur**:
   - Execute o seguinte comando para obter o URL do serviço do Conjur:
     ```sh
     kubectl get svc -n conjur
     ```
   - Anote o `EXTERNAL-IP` associado ao serviço `conjur`.

2. **Acesse o Painel do Conjur**:
   - Abra um navegador web e acesse o URL no formato `https://<EXTERNAL-IP>`.

3. **Faça Login no Conjur**:
   - Use as credenciais configuradas durante a instalação para fazer login no painel do Conjur.

4. **Verifique o Status do Conjur**:
   - Você também pode verificar o status dos pods do Conjur executando:
     ```sh
     kubectl get pods -n conjur
     ```

5. **Configuração Adicional**:
   - Dependendo da configuração do seu ambiente, você pode precisar configurar certificados SSL, ingress controllers, ou outras configurações de rede.



### OBSERVAÇÃO
   - O ansible não consegue fazer logout e login, e se faz necessário esse passo apos a vincular o usuario ao grupo libvirt, você pode estar configurado essa primeira etapa manualmente, ou separando em dois playbooks, ou rodando esse playbook aqui duas vezes, porém antes de rodar pela segunda vez se faz necessário realizar logout e login novamente para que as mudanças tenham efeito. Depois disso, execute o playbook novamente para continuar a configuração do ambiente OpenShift com CodeReady Containers e Conjur.

**Obtenção da Pull Secret**
   - Para obter a pull secret necessária para iniciar o CodeReady Containers (CRC), siga os passos abaixo:
      1. Acesse o portal do Red Hat Developers: Vá para [RedHat Developers](https://cloud.redhat.com/openshift/install/crc/installer-provisioned)
      2. Faça login: Use suas credenciais para acessar sua conta.
      3. Baixe a Pull Secret:
         - Procure pela opção de baixar a pull secret.
         - Clique na opção para criar uma nova pull secret.
         - Salve a pull secret em um arquivo chamado pull-secret.txt no seu sistema.