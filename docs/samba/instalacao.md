# Instalação do SAMBA

!!! note "Observações"

    - Documentação incompleta;
    - Faltou configurar o nome da máquina no formato FQDN;
    - Faltou o conteúdo do arquivo `/etc/samba/smb.conf`;
    - Faltou o comando que configura o servidor: `samba-tool domain provision`
    - Ausência de imagens que comprovassem a execução da tarefa.

## 1. Atualização do sistema

```bash
apk update
apk upgrade
```

## 2. Instalação do Samba e dos pacotes de dependências necessárias

```bash
apk add samba samba-dc krb5-server krb5-libs bind-tools
```

## 3. Configuração do Kerberos

Editar o arquivo `/etc/krb5.conf` com o seguinte conteúdo:

```bash
[libdefaults]
    default_realm = ES.LAB
    dns_lookup_realm = false
    dns_lookup_kdc = true

[realms]
    ES.LAB = {
        kdc = your-server.es.lab
        admin_server = your-server.es.lab
    }

[domain_realm]
    .es.lab = ES.LAB
    es.lab = ES.LAB
```

## 4. Configuração do Samba

Para provisionar o domínio para que o Samba atue como controlador de domínio do Active Directory, primeiro, o serviço do Samba deve ser parado se ele estiver rodando:

```bash
rc-service samba stop
```

Em seguida, remover qualquer configuração antiga do Samba que possa estar presente:

```bash
rm -rf /var/lib/samba/private/*
rm -rf /etc/samba/smb.conf
```

Agora, iniciar o processo de provisionamento:

```bash
samba-tool domain provision --use-rfc2307 --interactive
```

Durante o processo, as seguintes informações devem ser fornececidas:

- *Realm (domínio Kerberos)*: ES.LAB
- *Domínio NetBIOS*: ESLAB
- *Servidor DNS*: Escolher entre DNS interno ou externo (Bind, se já configurado).
- *Senha do administrador*: Escolher uma senha para o usuário Administrator.

Isso criará um novo arquivo de configuração `/etc/samba/smb.conf` automaticamente.

## 5. Iniciar o Samba após a configuração

```bash
rc-service samba start
```

## 6. Configurar para que os serviços do Samba iniciarem automaticamente após o boot

```bash
rc-update add samba
```

## 7. Verificar status 

Verificar se o servidor Samba está funcionando corretamente, mostrando assim os níveis funcionais do domínio e da floresta.

```bash
samba-tool domain level show
```

Além disso, verificar se o DNS e o Kerberos estão funcionando corretamente:

```bash
host -t SRV _kerberos._tcp.es.lab
host -t SRV _ldap._tcp.es.lab
```

#### 8. Gerenciamento de usuários e grupos

Adição de usuários e grupos ao domínio (serão gerenciados no controlador de domínio Samba) :

```bash
samba-tool user add <nome_do_usuario>
samba-tool group add <nome_do_grupo>
```

## Conclusão
Seguindo esses passos, o servidor Samba estará rodando como um controlador de domínio para o Active Directory no Alpine Linux com o domínio `es.lab`. A partir daqui, será possível conectar clientes Windows ao domínio, gerenciar políticas de grupo e configurar outras funcionalidades adicionais conforme necessário.