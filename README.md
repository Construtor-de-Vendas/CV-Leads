# API de Leads - v6.3
30 de Julho de 2019
## Contrutor de Vendas - CV19

# 1 INTRODUÇÃO

## 1.1 Definição
A interface viabiliza o cadastro e a modificação de leads para o sistema CV. As ações são executadas através do envio de um JSON, referente à requisição, contendo os dados dos campos a serem cadastrados ou modificados.

O cadastro pode ser proveniente do: (1) sistema CV - cadastro ou importação; (2) site do cliente; (3) integrações - RD Station, Facebook, Contako.

**Link para API:** https://[subdominio-cliente].construtordevendas.com.br/api/cvio/lead

## 1.2 Usuários
Os tipos de usuário que podem enviar requisições são:
  - **Gestor** (usuário administrativo) - pode cadastrar ou alterar todo e qualquer dado pertinente ao lead, estando a alteração restrita para os campos: (1) ação; (2) origem; (3) e-mail; (4) avatar - URL; (5) facebook; (6) twitter; (7) instagram; (8) interações; (9) módulo.
  - **Imobiliária** - pode cadastrar ou alterar todo e qualquer dado pertinente ao lead, estando a alteração restrita para os campos: (1) ação; (2) origem; (3) email; (4) avatar - URL; (5) facebook; (6) twitter; (7) instagram; (8) interações; (9) módulo; (10) imobiliária; (11) permitir alteração.
  - **Corretor** - pode cadastrar ou alterar todo e qualquer dado pertinente ao lead, estando a alteração restrita para os campos: (1) ação; (2) origem; (3) e-mail; (4) avatar - URL; (5) facebook; (6) twitter; (7) instagram; (8) interações; (9) módulo; (10) imobiliária; (11) corretor; (12) permitir alteração.

## 1.3 Influências
Pode haver uma cadeia de funcionalidades que influencia o lead, assim como um lead poderá influenciar uma cadeia de funcionalidades.

A cadeia de funcionalidades que influencia um lead é:  
  - **Empreendimentos** - um lead pode possuir um, vários ou nenhum empreendimento associado.
  - **Responsáveis** - um lead pode possuir como responsáveis: (1) uma imobiliária; e (2) um corretor, desde que esteja associado à imobiliária do lead.
  - **Propostas** - um lead pode possuir uma, várias ou nenhuma proposta associadas, desde que o e-mail ou telefone do lead possua alguma proposta vinculada.
  - **Interações** - um lead pode possuir uma, várias ou nenhuma interação cadastrada.
  - **Conversões** - um lead pode possuir uma, várias ou nenhuma conversão cadastrada.

Um lead não influencia nenhuma cadeia de funcionalidades.

# 2 ESPECIFICAÇÕES DA REQUISIÇÃO

## 2.1 Cabeçalho
| Nome | Descrição | Tipo | Obrg. | Tam. |
| ------ | ------ | ------ | ------ | ------ |
| E-mail ("email") | Informa o endereço de e-mail de login do usuário que executa a requisição (módulo). | String | Sim | 100 |
| Token ("token") | Informa o token ativo do usuário que executa a requisição (módulo). | String | Sim | 128 |

**Exemplo:**
```sh
{  
    "token": "2ed820f89afa16cabb6f1585f9a85b4e6bfc80c3"   
}
```

## 2.2 Corpo
| Nome | Descrição | Tipo | Obrg. | Tam. | Observação |
| ------ | ---------- | ------ | -- | -- | ------ |
| Ação ("acao") | Informa o tipo de ação que deve ser executada “cadastrar” ou “alterar”. | String | Sim | 100 |
| Nome ("nome") | Informa o nome do cliente do lead. | String | Sim | 100 |
| E-mail ("email") | Informa o endereço de e-mail cadastrado no lead. | String | Sim | 100 |
| Telefone ("telefone") | Informa o número de telefone cadastrado no lead. | String | Não | 15 | Restrição numérica e máscara para campo de telefone.
| Facebook ("facebook") | Informa perfil da rede social do cliente ou associado. | String | Não | 100 |
| Twitter ("twitter") | Informa perfil da rede social do cliente ou associado. | String | Não | 100 |
| Instagram ("instagram") | Informa perfil da rede social do cliente ou associado. | String | Não | 100 |
| Avatar ("url_avatar") | Fornece a foto ou logo do cliente do lead. | String | não | 100 | Enviado através de URL.
| Empreendimento ("idempreendimento") | Informa o(s) empreendimento(s) de interesse do lead. | Integer | Não | 10 | Pode ser enviado apenas um ID ou um array contendo vários IDs.
| Permitir alteração ("permitir_alteracao":"true") | Permitite alterar / incluir informações no lead (Nome, e-mail, telefone e campos adicionais) caso o lead já exista cadastrado. | Boolean | Sim | - |
| Ponto de Venda ("idpdv") | Informa o ponto de venda associado ao lead. | Integer | Não | 10 | Pode ser enviado apenas um ID.
| Imobiliária ("idimobiliaria") | Informa a imobiliária (ID) que será vinculada ao lead. | Integer | Não | 10 | 
| Data de Associação da Imobiliária ("data_associacao_imobiliaria") | Informa a data em que a imobiliária foi vinculada ao lead. | Datetime | Não | - | 
| Corretor ("idcorretor") | Informa o corretor (ID) que será vinculado ao lead. | Integer | Não | 10 | 
| Corretor ("email_corretor") | Informa o e-mail do corretor que será vinculado ao lead. Uma alternativa para caso o usuário não saiba qual id de corretor passar. | String | Não | 100 | 
| Data de Associação do Corretor ("data_associacao_corretor") | Informa a data em que o corretor foi vinculado ao lead. | Datetime | Não | - | 
| Situação ("idsituacao") | Informa a situação (ID) do lead. | Integer | Não | 10 |
| Responsável ("idusuario") | Informa o usuário administrativo que será vinculado ao lead como responsável. | Integer | Não | 10 | 
| Responsável ("email_gestor") | Informa o e-mail do usuário administrativo que será vinculado ao lead como responsável. Uma alternativa para caso o usuário não saiba qual id de usuário administrativo passar. | String | Não | 100 | 
| Origem ("origem") | Informa a origem (ID) do lead. | String | Não | 2 | Opções - "ND" - Não Definido / "GE" - Painel Gestor / "CO" - Painel Corretor / "IM" - Painel Imobiliária / "FB" - Facebook Ads / "SI" - WebSite / "GO' - Google / "CH" - Chat Online / "TD" - Tráfego Direto / "MP" - Mídia Paga / "BO" - Busca Orgânica / "EM" - Email / "RF" - Referência / "SC" - Social / "DP" - Display / "OP" - Outras publicidades / "OU" - Outros / "UK" - Desconhecido. Caso não seja enviado no JSON da requisição, recebe o valor padrão do sistema (o valor do campo “modulo”).
| Mídia ("midia") | Informa o código da mídia que está gerando o lead. | Integer | Não | 0 | Ex.: gpc, ads
| Data do Vencimento ("data_vencimento") | Informa a data de vencimento do lead de acordo com a situação atual. | Datetime | Não | 0 | Deve ser enviado no formato BR.
| Utilizar fila ("lead_utilizar_fila") | Substitui a variável do específico de utilização da Fila de imobiliárias e corretores. | Boleano | Não |  |
| Conversão ("conversao") | Informa o nome da fonte de uma nova entrada de um lead existente. | String | Não | 100 |
| Data da Conversão ("data_cad_conversao") | Informa a data que a conversão do lead foi cadastrada. | Datetime | Não | 0 | Deve ser enviado no formato BR.
| Campos Adicionais ("campos_adicionais") | Informa o(s) campo(s) extra(s) e seu(s) respectivo(s) valor(es), cadastrado(s) por uma construtora. | String / Text | Não | 100 |
| Interações ("interacoes") | Informa as interações (anotação, ligação, e-mail, SMS, WhatsApp) que foram efetuadas no lead. | String / Text | Não | 1 / 0 | Array de arrays contendo os campos “tipo” e “descricao” para cada interação. Opções - “A” (anotação) / “L” (ligação) / “E” (e-mail) / “S” (SMS) / “W” (WhatsApp).

**Exemplo:**
```sh
{   
    "acao": "salvar",
    "nome": "Nivaldo Oliva II",
    "email": "nivaldoolivasegundo@gmail.com",
    "telefone": "(79) 98833-0011",
    "permitir_alteracao":"true",
    "idempreendimento": 
    {
        "0":30
    },
    "origem": "SI",
    "conversao": "Campanha 2018.10.31",
    "campos_adicionais": 
    {
        "possui_imoveis": "Sim"
    },
    "interacoes": 
    {
        "0": 
        { 
            "tipo" : "L",
            "descricao" : "Ligar para Alfred Ramos"
        },
        "1": 
        { 
            "tipo" : "W",
            "descricao" : "Teste de mensagem pelo WhatsApp"
        }
    }
}
```

## 2.3 Resposta (mensagem de sucesso)
| Nome | Descrição | Tipo | Obrg. | Tam. | Observação |
| ------ | ---------- | ------ | -- | -- | ------ |
Sucesso ("sucesso") | Retorna se a ação de “cadastrar” ou “alterar” foi efetuada com sucesso ou não. | String |  | 10 | Opções - “True” / “False”. |
Lead ("id") | Retorna o lead (ID) que foi cadastrado ou alterado. | Integer |  | 10
Imobiliária ("idimobiliaria") | Retorna a imobiliária (ID) do lead cadastrado ou alterado. | Integer |  | 10 | No caso de uma requisição enviada pelo módulo “gestor”. |
Nome da Imobiliária ("imobiliaria_nome") | Retorna o nome da imobiliária do lead cadastrado ou alterado. | String |  | 40 | Imobiliária do Lead |
E-mail da Imobiliária ("imobiliaria_email") | Retorna o email da imobiliária do lead cadastrado ou alterado. | String |  | 40 | email@imobiliaria.com.br |
Telefone da Imobiliária ("imobiliaria_telefone") | Retorna o telefone da imobiliária do lead cadastrado ou alterado. | String |  | 40 | (79) 99873-8818 |
Corretor ("idcorretor") | Retorna o corretor (ID) do lead cadastrado ou alterado. | Integer |  | 10 | No caso de uma requisição enviada pelo módulo “gestor” ou “imobiliária”. |
Referência do corretor ("corretor_referencia") | Retorna a referência do corretor do lead cadastrado ou alterado. | String |  | 40 | COR390 |
Nome do corretor ("corretor_nome") | Retorna o nome do corretor do lead cadastrado ou alterado. | String |  | 40 | Corretor do Lead |
E-mail do Corretor ("corretor_email") | Retorna o email do Corretor do lead cadastrado ou alterado. | String |  | 40 | email@corretor.com.br |
Telefone do Corretor ("corretor_telefone") | Retorna o telefone do Corretor do lead cadastrado ou alterado. | String |  | 40 | (79) 99873-8818 |
Usuário Gestor ("idusuario") | Retorna o usuario atendente (ID) do lead cadastrado ou alterado. | Integer |  | 10 | No caso de uma requisição enviada pelo módulo “gestor” ou “imobiliária”. |
Nome do Usuário ("usuario_nome") | Retorna o nome do usuário do lead cadastrado ou alterado. | String |  | 40 | Usuário do Lead |
E-mail do Usuário ("usuario_email") | Retorna o email do Usuário do lead cadastrado ou alterado. | String |  | 40 | email@usuario.com.br |
Telefone do Usuário ("usuario_telefone") | Retorna o telefone do Usuário do lead cadastrado ou alterado. | String |  | 40 | (79) 99873-8818 |
Situação ("idsituacao") | Retorna a situação (ID) do lead cadastrado ou alterado. | Integer |  | 10 |
Mensagem ("mensagem") | Retorna a ação que foi efetuado no lead. | String |  | 100 | Opções - “cadastrou_sucesso” / “modificou_sucesso”.
Código ("codigo") | Retorna o response code referente ao resultado da ação efetuada no lead. | Integer |  | 3 |

**Exemplo:**
```sh
{   
    "sucesso": true,
    "id": 82,
    "idimobiliaria": "2",
    *"imobiliaria_nome": "Imobiliária do Lead",
    *"imobiliaria_email": "email@imobiliaria.com.br",
    *"imobiliaria_telefone": "(79) 998738818",
    "idcorretor": "4",
    *"corretor_referencia": "COR390",
    *"corretor_nome": "Corretor do Lead",
    *"corretor_email": "email@corretor.com.br",
    *"corretor_telefone": "(79) 998738818",
    *"idusuario": "4",
    *"usuario_nome": "Atendente do Lead",
    *"usuario_email": "email@usuario.com.br",
    *"usuario_telefone": "(79) 998738818",
    "idsituacao": "3",
    "mensagem": "cadastrou_sucesso",
    "codigo": 200  
}
```

# 3 ESPECIFICAÇÕES DAS AÇÕES

## 3.1 Cadastro de leads
O cadastro de um lead é efetuado utilizando dois campos principais: (1) e-mail; (2) telefone. Um lead pode ser cadastrado mediante a três situações desses campos: (1) com e-mail e telefone; (2) apenas com e-mail; (3) apenas com telefone.

Caso o JSON da requisição de cadastro do lead possua o campo “e-mail” e o campo “telefone”, o lead é cadastrado e o campo “e-mail” será sua chave. O campo “e-mail” possui prioridade em relação ao campo “telefone”, desta forma leads diferentes podem ter o mesmo número de telefone desde que tenham e-mails diferentes.

Caso o JSON da requisição de cadastro do lead possua apenas o campo “e-mail”, o lead é cadastrado deixando o campo “telefone” vazio e, da mesma forma, o campo “e-mail” será sua chave. Não podem existir dois ou mais leads no sistema que tenham o mesmo e-mail.

Caso o JSON da requisição de cadastro do lead possua apenas o campo “telefone”, o lead é cadastrado deixando o campo “e-mail” vazio e o campo “telefone” será sua chave. Não podem existir dois ou mais leads no sistema que não possuem e-mail e tenham o mesmo número de telefone. Leads diferentes podem ter o mesmo número de telefone desde que tenham e-mails diferentes.

## 3.2 Situação
Ao cadastrar um novo lead é verificado se o JSON da requisição possui o campo “idsituacao” preenchido: (1) caso o valor seja nulo, a situação do lead deve ser cadastrada com a flag “início”; (2) caso o valor seja diferente de nulo, a situação do lead deve ser cadastrada com o novo valor enviado; (3) caso não possua um valor, segue para a verificação do próximo campo e será cadastrada com a flag “início”. Os casos descritos anteriormente não serão aplicados: (1) se for enviado um idcorretor, neste caso será cadastrado na situação com flag "corretor"; (2) se o e-mail ou telefone estiver vinculado a qualquer reserva existente no sistema CV, neste caso será cadastrado na situação com flag "proposta".

Ao editar um lead é verificado se o JSON da requisição possui o campo “idsituacao” preenchido: (1) caso o valor seja nulo e a situação atual do lead seja “cancelado”, então a situação do lead deve ser modificada para “início”; (2) caso o valor seja diferente de nulo, a situação do lead deve ser modificada para o novo valor enviado; (3) caso não possua um valor, a situação permanece a mesma e segue para a verificação do próximo campo.

## 3.3 Empreendimentos
Ao cadastrar um novo lead ou editar um lead existente é verificado se o JSON da requisição possui o campo “idempreendimento” preenchido: (1) caso exista um ou mais valores, adiciona ao lead apenas os valores que estiverem ativos tanto no banco de dados quanto no painel; (2) caso não possua um valor, segue para a verificação do próximo campo.

## 3.4 Responsável
Ao cadastrar um novo lead ou editar um lead existente é verificado se o JSON da requisição possui o campo “idimobiliaria” ou “idcorretor” preenchido: (1.1) caso a requisição tenha sido enviada pelo módulo “gestor”, adiciona a nova imobiliária ao lead; (1.2) caso a requisição tenha sido enviada pelo módulo “gestor”, se o corretor estiver vinculado a imobiliária, adiciona o novo corretor ao lead; (2) caso a requisição tenha sido enviada pelo módulo “imobiliária”, se o corretor estiver vinculado a imobiliária, adiciona o novo corretor ao lead; (3) caso não possua um valor, segue para a verificação do próximo campo.

## 3.5 Propostas
Ao cadastrar um novo lead é verificado se o e-mail ou o telefone no JSON da requisição pertence a alguma proposta (reserva) existente no sistema CV, seja como titular ou associado da mesma. Existindo uma ou mais propostas elas devem ser associadas ao lead. 

Durante essa ação, a situação do lead só deve ser alterada para “reserva”, caso uma das propostas associadas tenha a situação diferente de: (1) vendido; (2) distrato; (3) cancelado; ou (4) vencido. 

Ao editar um lead existente é verificado se o e-mail ou o telefone no JSON da requisição pertence a alguma proposta (reserva) existente no sistema CV, seja como titular ou associado da mesma. Existindo uma ou mais propostas elas devem ser associadas ao lead. 

Durante essa ação, a situação do lead só deve ser alterada para “reserva”, caso uma das propostas associadas tenha a situação diferente de: (1) distrato; (2) cancelado; ou (3) vencido. Havendo uma proposta com situação igual a “vendido”, a situação do lead deve ser alterada para “finalizado”.

## 3.6 Origem
Ao cadastrar um lead: (1) caso seja enviado o campo “origem” no JSON da requisição, ele será cadastrado como a origem do lead; (2) caso não exista uma “origem” no JSON da requisição, a origem do lead deve ser o padrão do sistema (o valor do campo “módulo”).

Desta forma, a “origem” de um lead sempre será preenchida de alguma forma. A origem de um lead é única e não pode ser editada.

Ao editar um lead, caso seja enviado o campo “origem” no JSON da requisição, ele deve ser tratado como a origem de uma conversão.

## 3.7 Conversão
Ao cadastrar um lead, uma “conversão” pode ser enviada no JSON da requisição. Caso seja enviada uma “conversão”, sua origem será a mesma origem do lead. 

Ao cadastrar ou editar um lead, caso seja enviada uma “conversão” que ainda não exista no sistema, ela será cadastrada. Existe um CRUD para registrar conversões. Se uma conversão for enviada no JSON da requisição com o nome diferente de alguma conversão já registrada no sistema, então ela será cadastrada como uma nova conversão.

Ao editar um lead, uma “conversão” pode ser enviada no JSON da requisição: (1) caso seja enviado um campo “conversão” e um campo “origem”, essa origem deve ser tratada como a origem da conversão; (2) caso seja enviada uma “conversão” sem uma “origem”, essa “conversão” terá sua “origem” estabelecida como “Não definida”.

## 3.8 Interações
Ao cadastrar um novo lead ou editar um lead existente é verificado se o JSON da requisição possui o campo “interacoes” preenchido: (1) caso exista um ou mais valores, adiciona a(s) interação(ões) ao lead, com seus respectivos valores de “tipo” e “descricao”; (2) caso não possua um valor, segue para a verificação do próximo campo.

## 3.9 Avatar
Ao cadastrar um lead, o avatar pode cadastrado por: (1) importação através do e-mail; (2) URL de uma imagem.

No caso de buscas através do e-mail (Gmail) pela API de imagem, o avatar não será padrão para todos os clientes, depende de uma flag no sistema CV. Se a flag estiver definida para não efetuar buscas, o avatar ficará como as iniciais do nome do lead. Do contrário, será importada a mesma imagem utilizada na conta de e-mail.

Ao editar um lead, a imagem do avatar só pode ser alterada: (1) por integração, via URL (endereço da imagem); ou (2) através de nova requisição para o mesmo e-mail (API de imagem) que teve sua imagem modificada.

## 3.10 Ponto de Venda
Ao cadastrar um lead pela API, pode ser enviado o campo “idpdv” no JSON da requisição. Neste caso não existe uma verificação específica e o PDV é cadastrado no lead.

Ao editar um lead pela API, pode ser enviado o campo “idpdv” no JSON da requisição. Caso seja enviado, as situações possíveis são: (1) se o PDV está associado à imobiliária do lead ou a algum empreendimento do lead, será cadastrado no lead, do contrário não; (2) caso não exista nem imobilária nem empreendimentos associados ao lead, o PDV será cadastrado no lead; (3) caso seja enviado o mesmo “idpdv” nada será alterado.

Caso um PDV não possua associação com uma imobiliária nem com algum empreendimento, ele deverá ser exibido em todos os painéis.
