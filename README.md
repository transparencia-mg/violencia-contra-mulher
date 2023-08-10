# Conjunto de dados - Dataset

Este dataset template é um conjunto de automatizações desenvolvidas pela Diretoria Central de Transparência Ativa - DCTA/CGE para criação, documentação, validação e publicação (criação e atualização em instâncias do CKAN) de conjunto de dados ou datasets.

Para esclarecimento sobre o fluxo completo de abertura de dados, favor consultar o [Manual do Portal de Dados Abertos de Minas Gerais](https://transparencia-mg.github.io/manual-dados-mg).

### Funcionalidades:

- Documentação de acordo com especificação de qualidade de metadados sem fricção ([fricitonless](https://specs.frictionlessdata.io/#overview)).
- Controle de versões da documentação e dos dados via Git e GitHub.
- Conversão automatizada de base de dados em Excel para formato tabular aberto (csv), caso necessário.
- Validação automatizada dos metadados e dos dados do conjunto, com demonstração de erros de validação, caso haja.
- Publicação automatizada (criação e atualização em instâncias do CKAN) do conjunto criado, documentado e validado.

### Como participar

A configuração deste dataset template está sendo feita de forma aberta e colaborativa no [GitHub](https://github.com/transparencia-mg/new-dataset-template).
Existem duas alternativas para enviar sua contribuição:

- [Issues](https://github.com/transparencia-mg/new-dataset-template/issues): Para iniciar uma discussão sobre melhorias de funcionalidades.
- [Pull requests](https://github.com/transparencia-mg/new-dataset-template/pulls): Para sugerir uma alteração concreta na ferramenta.

Todas as contribuições são bem vindas. Alguns exemplos são:

* Indicação de expressões imprecisas presentes na documentação;
* Sugestões para inclusão de descrições em campos específicos;
* Sugestões para clareza na organização das ideias;
* Correção de erros de ortografia e gramática.

### Fluxo de execução

```mermaid
graph TD;
    1(Início)-->2;
    2[Forcar dataset template]-->3;
    3[Cadastrar secrets]-->4;
    4[Configurar github pages]-->5;
    5[Incluir arquivo .xls na pasta upload]-->6;
    6[Script publica novo conjunto no CKAN]-->7;
    7(Fim)
```

### Setup do projeto

- **Todas as etapas de preparação da base de dados a ser publicada deverão estar finalizadas[^1] para realização dos passos descritos a seguir**.

- **Realize o fork do projeto** (utilizaremos um fork para conseguir atualizar as automatizações com maior facilidade no futuro):

![fork_projeto](https://imgur.com/uOZlh8a.png)

- Selecione a organização a qual o novo conjunto de dados será criado e preencha o nome do novo repositório (**o nome deverá ser o mesmo do conjunto que será criado na instância do CKAN**).

  OBS.: Certifique-se que o nome desejado para o novo conjunto não está sendo usando, pela lista dos conjuntos atualmente publicados [em ambiente de produção](https://dados.mg.gov.br/api/3/action/package_list) e [homologação](https://homologa.cge.mg.gov.br/api/3/action/package_list) ou pelas respectivas páginas dos conjuntos publicados: [produção](https://dados.mg.gov.br/dataset/) e [homologação](https://homologa.cge.mg.gov.br/dataset/)

![fork_org_name](https://imgur.com/bqSjsyQ.png)

- **Cadastre Secrets para publicação em instância CKAN**:

![fork_settings](https://imgur.com/I3OFQwu.png)

![fork_secrets](https://imgur.com/aan0HNd.png)

![fork_new_secrets](https://imgur.com/Xg2TLCd.png)

- **Deverão ser criadas três secrets**:
    - OWNER_ORG: Organização dentro da instância do CKAN desejada a qual o conjunto de dados será vinculado (nome disponível na url CKAN após `https://ckan-instance/organization/`), exemplos
      - `controladoria-geral-do-estado-cge` em https://dados.mg.gov.br/organization/controladoria-geral-do-estado-cge
      - `secretaria-de-estado-de-planejamento-e-gestao-seplag` em https://homologa.cge.mg.gov.br/organization/secretaria-de-estado-de-planejamento-e-gestao-seplag.

  OBS.: Certifique-se também de que seu usuário está cadastrado para a organização que deseja cadastrar o novo conjunto de dados, seja em [produção](https://dados.mg.gov.br/dashboard/organizations) em [homologação](https://homologa.cge.mg.gov.br/dashboard/organizations)

    - CKAN_HOST: Instância CKAN desejada, exemplo: `https://homologa.cge.mg.gov.br`
    - CKAN_KEY_USUARIOGITHUB: se meu usuário GitHub é `gabrielbdornas` este secret será `CKAN_KEY_GABRIELBDORNAS`. Para o `andrelamor`, o secret `CKAN_KEY_ANDRELAMOR`

        - **Necessário criar um novo API Token na instância CKAN desejada (copiar e colar o valor `API TOKEN created` da 4ª tela printada a seguir)**:

![ckan_chave](https://imgur.com/Dr1VxG8.png)

![ckan_chave_token](https://imgur.com/TpUQoLM.png)

![ckan_chave_nome](https://imgur.com/AwD8hgc.png)

![ckan_chave_criada](https://imgur.com/4qgD7HS.png)

- Cadastrar GitHub pages para mostrar relatório de validação:

![fork_settings](https://imgur.com/I3OFQwu.png)

![fork_pages](https://imgur.com/QMSmQ78.png)

![fork_pages](https://imgur.com/dHStfzi.png)

![image](https://github.com/transparencia-mg/new-dataset-template/assets/49699290/f66216ef-4faa-426d-8d49-002dcb5b9de0)

- Configurar GitHub pages para link aparecer na página inicial do repositório:

![pages](https://imgur.com/VtduVFv.png)

![pages](https://imgur.com/TYN8J2Z.png)

- Configurar permissão para Actions ler e escrever no repositório:

  OBS.: Caso a permissão para Actions ler e escrever no repositório não esteja habilitada, esta configuração deverá ser feita também no nível da organização.

![fork_settings](https://imgur.com/I3OFQwu.png)

![image](https://github.com/transparencia-mg/new-dataset-template/assets/49699290/7e5f739a-1b15-4bd1-a225-1cd75655d80b)

- Para rodar o processo automatizado basta incluir base de dados a ser aberta na pasta `upload`, dentro da pasta `dataset` do novo repositório forkado e configurado:

![image](https://github.com/transparencia-mg/new-dataset-template/assets/52294411/f70225bc-a887-479e-bf1e-dacfc4975004)

![image](https://github.com/transparencia-mg/new-dataset-template/assets/52294411/7830e2fb-b2bf-434c-87b3-e366e5efa7a1)

## Atualizações

Nos repositórios forkados do new-dataset-template, observar se há commits do repositório template para serem sincronizados:
![image](https://github.com/transparencia-mg/new-dataset-template/assets/52294411/060715a7-e1e1-43a3-9a76-9286f20b4807)
Basta clicar em `Sync fork`e, depois, no botão `update branch`:
![image](https://github.com/transparencia-mg/new-dataset-template/assets/52294411/82642ae9-7d97-4e84-9603-6701e4591cb6)
Aparecerá a mensagem na tarja superior em azul-claro:
![image](https://github.com/transparencia-mg/new-dataset-template/assets/52294411/5a259c7e-61ab-42cc-ae0e-dadce259778e)

Observe que o repositório clonado na máquina precisará do `pull`, para ser atualizado após esse sync, como qualquer alteração que ocorre no github.

Clicando em `Fork`, é possível listar todos os repositórios que foram gerados a partir do new-dataset-template, e conferir um por um:
![image](https://github.com/transparencia-mg/new-dataset-template/assets/52294411/55a59bac-d1b4-4383-ad0d-cb5dcfc5ac3d)


[^1]: [Ciclo de Abertura, Documentação, Validação e Publicação](https://transparencia-mg.github.io/manual-dados-mg/0.1/2.%20Ciclo%20de%20publica%C3%A7%C3%A3o%20de%20dados/006_etapas_abertura/).
