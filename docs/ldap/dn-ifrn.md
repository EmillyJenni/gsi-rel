# Explicação de seu DN do LDAP no IFRN

## O DN do usuário é:

`CN=20221148060021,OU=Alunos,OU=DG-PAR,OU=RE,OU=IFRN,DC=ifrn,DC=local`

## 1. DN (Distinguished Name):
O DN (Nome Distinto) é o identificador completo de um objeto em uma árvore LDAP. Ele é composto de uma sequência de Relatively Distinguished Names (RDNs), que identificam o objeto de forma única dentro do domínio. No caso do usuário, o DN completo é:

`CN=20221148060021,OU=Alunos,OU=DG-PAR,OU=RE,OU=IFRN,DC=ifrn,DC=local`

Este DN indica o caminho completo para localizar o usuário 20221148060021 na árvore LDAP.

## 2. RDN (Relative Distinguished Name):
O RDN (Nome Relativo Distinto) é o componente do DN que identifica exclusivamente o objeto dentro do seu contexto imediato. No DN fornecido, o RDN do usuário é:

`CN=20221148060021`

Aqui, CN (Common Name) representa o nome do objeto (usuário). Portanto, o RDN diz que o nome do usuário é 20221148060021 dentro do contêiner onde ele está localizado.

## 3. DC (Domain Component):
O DC (Componente de Domínio) é utilizado para identificar os diferentes níveis de um domínio no LDAP. No caso fornecido, os componentes de domínio são:

`DC=ifrn, DC=local`

Isso define o domínio em que o objeto (usuário) está. Esse domínio corresponde ao nome DNS ifrn.local.

- DC=ifrn: Especifica o domínio principal "ifrn".
- DC=local: Especifica que o domínio está no namespace .local.

## 4. OU (Organizational Unit):
O *OU* (Unidade Organizacional) é uma subdivisão dentro do domínio, usada para organizar objetos em grupos hierárquicos. No DN fornecido, o usuário está dentro de várias Unidades Organizacionais (OUs), que formam uma hierarquia:

`OU=Alunos,OU=DG-PAR,OU=RE,OU=IFRN`

Cada uma dessas OUs refina o local onde o usuário está armazenado:

- OU=Alunos: Indica que o usuário pertence à unidade organizacional de alunos.
- OU=DG-PAR: Especifica outra subunidade dentro de "Alunos", provavelmente relacionada à Direção Geral ou algum departamento específico.
- OU=RE: Pode se referir a uma Regional, como uma subdivisão administrativa.
- OU=IFRN: Indica que essa unidade organizacional está dentro do Instituto Federal do Rio Grande do Norte (IFRN).

## Conclusão
Esse DN completo descreve a posição exata do usuário 20221148060021 dentro da hierarquia da árvore LDAP no domínio ifrn.local, passando por várias unidades organizacionais até chegar ao usuário.