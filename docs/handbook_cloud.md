---
id: handbook_cloud
title: Handbook Cloud
---

## Briefing para novos projetos

* Cartão de crédito deles?
* Local da infra, SP ou N. Virginia?
* Domínios utilizados;
* Acesso aos Registro.br dos dominios (contato técnico para HNILT3);
* DNS, vai ficar por nossa conta? (Se não, passar contato técnico do responsável);

## Checklist de conta herdada

Algumas vezes nós acabamos herdando uma conta ao invés de iniciarmos ela do zero, existem alguns pontos interessantes para adaptarmos/conferirmos:

* Não usar instâncias do tipo “T”, pois, elas possuem um limite de conexão muito baixo (~100), quando comparadas com instâncias de outros tipos;
* Conferir o horário da janela de manutenção do RDS;
* Limpar os IP’s liberados nas EC2;
* Limpar os acessos via IAM da conta;
* Limpar o(s) arquivo(s) .ssh/authorized_keys das EC2; 

## Magento 2
* [Magento Hardware Recomendations](https://devdocs.magento.com/guides/v2.3/performance-best-practices/hardware.html);
* [Magento Software Recomendations](https://devdocs.magento.com/guides/v2.3/performance-best-practices/software.html);
* [Magento Configuration Recomendations](https://devdocs.magento.com/guides/v2.3/performance-best-practices/configuration.html);
* Sessions em Redis ou em um FS montado na RAM (tmpfs)
    * Quando usar Redis como o session backend é importante lembrar de habilitar o **disable_locking**, tem um [artigo monstruoso](https://willparsons.tech/redis-session-locking/) sobre isso (também tem uma [issue](https://github.com/magento/magento2/issues/17310#issuecomment-470932848) no github sobre isso) - *Em nossos testes quando essa lock  fica ligada realmente temos problemas, desde 503 principalmente quando tentamos tirar um produto do carrinho, para usleep’s (pegos no blackfire.io), de 500ms nas requisições ajax deixando tudo lento*;
* Configurar o session garbage collector do PHP (session.gc_probability e session.gc_divisor)

## Métricas chave

* Network Mpbs (alerta quando acima de 200 Mpbs);

## Configurações MySQL

| Config             | Default | Recomendado |
| ------------------ | ------- | ----------- |
| max_allowed_packet | 4MB     | 16/32 MB    |

## FAQ

**Como pegar dados de umas instância AWS EC2, dentro dela (via SSH)?**  
R: Dentra da instância temos um [endpoint especial de metadados](https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/ec2-instance-metadata.html) que retorna todos os dados da própria instância. [Aqui](https://docs.aws.amazon.com/pt_br/AWSEC2/latest/UserGuide/ec2-instance-metadata.html#instancedata-data-categories) temos uma listagem de todas as categorias que podemos pegar.

**Resetar o password da conta master de um RDS produz downtime?**  
R: Não, mas é recomendado efetuar essa operação em uma janela de manutenção.

**Conseguimos mudar configurações na mão com “SET GLOBAL <config>=<value>” no AWS RDS?**  
R: Não, todas as mudanças de configuração de um banco de dados devem ser feitas via parameter group. Suporte da AWS explica isso nessa [thread](https://forums.aws.amazon.com/thread.jspa?threadID=37852) do fórum.

**Mudar uma configuração de um parameter group que já está aplicado no RDS produz downtime?**  
R: Quando modificamos o RDS devemos ter atenção nas propriedades do parâmetro a ser alterado, sabemos que pode ter diferenças entre parâmetros e alguns deles talvez possam produzir downtime. Antes de qualquer alteração devemos observar [esta lista](https://dev.mysql.com/doc/refman/5.6/en/server-system-variables.html), onde os parâmetros do tipo dynamic não causam parada, os do tipo static necessitam de reboot da instância.

## Analisar depois e incluir aqui

* Guide Magento 2 na AWS:
    * https://aws.amazon.com/pt/quickstart/architecture/magento/
    * https://docs.aws.amazon.com/pt_br/quickstart/latest/magento/welcome.html
    * https://github.com/aws-quickstart/quickstart-magento
