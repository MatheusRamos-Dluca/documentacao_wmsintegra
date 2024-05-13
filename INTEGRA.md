# WMSExpert Integra
**Documentação de integração WMSExpert**

# Autenticação <br />

> É o primeiro processo que tem que ser feito para poder usar a api. Ela retornará o token de acesso fundamental para o funcionamento e segurança da aplicação.

```
    post: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/auth   
```

> corpo da requisição. Todos os campos não apresetação tamanho minímo ou máximo, apenas estarem cadastrados no sistema.  

```
    {
    "login" : string,
    "senha" : string,
    "filial" : interger
    }

```

# Produtos

### Lista de Produtos </br>

> O método de envio para pegar os produtos cadastros no sistema. URL de envio e o método de envio correspondente.

```
    get: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/produto/geral   
```

> A api retornará uma lista de produtos na seguinte estrutura.


```
[
    {
        "altura": integer,
        "codigo": string,
        "codigoref": string,
        "controlalote": boolean,
        "controlanumserie": boolean,
        "controlavalidade": boolean,
        "empresa": integer,
        "endereco": integer,
        "estoquemaximo": integer,
        "estoqueminimo": integer,
        "fornecedor": integer,
        "grupo": integer,
        "id": integer,
        "lastro": integer,
        "nome": string,
        "pesobruto": integer,
        "pesoliquido": integer,
        "shelflife": integer,
        "subgrupo": integer,
        "unidadepadrao": string
    }
]
```

> ### View de clientes WMS_CLIENTE

``` 
CREATE VIEW WMS_CLIENTE AS 
SELECT 
codClienteErp,
tipo,
cpfCnpj,
nomCliente,
nomFantasia,
codCidadeIbge,
endereco,
numEndereco,
bairro,
cep,
celular,
email,
codRota,
desRota,
latitude,
longitude,
shelf
FROM CLIENTES
```

**codClienteErp:** *O campo deve ser **varchar(20)**, contendo o codigo do cliente do ERP o campo e chave primaria e **obrigatorio**.* <br />
**tipo:** *O campo deve ser **inteiro** contendo 0 para pessoa fisica e 1 para pessoa juridica o campo e **obrigatorio**.* <br />
**cpfCnpj:** *O campo deve ser **varchar(14)** contendo a inscrição da pessoa fisica ou juridica o campo e **obrigatorio**.* <br />
**nomCliente:** *O campo deve ser **varchar(60)** contendo a razão social do cliente o campo e **obrigatorio**.* <br />
**nomFantasia:** *O campo deve ser **varchar(60)** contendo o nome fantasia do cliente o campo e **obrigatorio**.* <br />
**codCidadeIBGE:** *O campo deve ser **inteiro**, o mesmo e chave primaria o campo e **obrigatorio**.* <br />
**endereco:** *O campo deve ser **varchar(60)** contendo o endereço do cliente o campo e **obrigatorio**.* <br />
**numEndereco:** *O campo deve ser **varchar(10)** contendo o numero do endereço do cliente o campo e **obrigatorio**.* <br />
**bairro:** *O campo deve ser **varchar(30)** contendo a descrição do bairro do cliente o campo e **obrigatorio**.* <br />
**cep:** *O campo deve ser **varchar(8)** contendo o contendo o codigo postal do cliente o campo e **obrigatorio**.* <br />
**celular:** *O campo deve ser **varchar(10)** contendo o telefone do cliente.* <br />
**email:** *O campo deve ser **varchar(50)** contendo o e-mail do cliente.* <br />
**codRota:** *O campo deve ser **inteiro** contendo o codigo da rota.* <br />
**desRota:** *O campo deve ser **varchar(60)** contendo a descrição da rota.* <br />
**latitude:** *O campo deve ser **numeric(18,7)** contendo a latitudo do cliente.* <br />
**longitude:** *O campo deve ser **numeric(18,7)** contendo a longitude do cliente.* <br />
**shelf:** *O campo deve ser **inteiro** contendo a quantidade de dias do shelf do cliente.* <br /><br />


> ### View de embalagens WMS_EMBALAGEM

``` 
CREATE VIEW WMS_EMBALAGEM AS 
SELECT 
codEmbalagem,
codFilial,
codProdutoErp,
aux,
und,
qtdUnit,
embalagem,
pesoLiquido,
pesoBruto,
volume,
Ativo
FROM EMBALAGENS
```

**codEmbalagem:** *Enviar o campo como **NULL**.* <br />
**codFilial:** *O campo deve ser **inteiro**, o mesmo e chave primaria o campo e **obrigatorio**.* <br />
**codProdutoErp:** *O campo deve possuir a chave estrangeira do produto o campo e **obrigatorio**.* <br />
**aux:** *O campo deve ser **varchar(20)** contendo o codigo de barras do produto o campo e **obrigatorio**.* <br />
**und:** *O campo deve ser **varchar(3)** contendo a descrição reduzida da embalagem o campo e **obrigatorio**.* <br />
**qtdUnit:** *O campo deve ser **numerico(12,2)**, contendo o fator de conversão da unidade o campo e **obrigatorio** e tem de ser diferente de zero.* <br />
**embalagem:** *O campo deve ser **varchar(20)** contendo a descrição da embalagem o campo e **obrigatorio**.* <br />
**pesoLiquido:** *O campo deve ser **numeric(18,4)** contendo o peso liquido da embalagem.* <br />
**pesoBruto:** *O campo deve ser **numeric(18,4** contendo o peso bruto da embalagem.* <br />
**volume:** *O campo deve ser **numeric(18,2)** contendo a o volume em **m3** da embalagem.* <br />
**ativo:** *O campo deve ser **inteiro** contendo 1 para ativo e 0 para inativo o campo e **obrigatorio**.* <br /><br />

> ### View de estoque WMS_ESTOQUE

``` 
CREATE VIEW WMS_ESTOQUE AS 
SELECT 
codFilialErp,
codProdutoErp,
qtdEstoque,
lote,
validade,
numeroSerie
FROM ESTOQUE
```

**codFilialErp:** *O campo deve ser **inteiro**, o mesmo e chave primaria o campo e **obrigatorio**.* <br />
**codProdutoErp:** *Chave estrangeira do codigo do produto o campo e **obrigatorio**.* <br />
**qtdEstoque:** *O campo deve ser **numerico(18,2)**, contendo a quantidade de estoque do produto o campo e **obrigatorio**.* <br />
**lote:** *O campo deve ser **varchar(50)**, contendo o lote do produto.* <br />
**validade:** *O campo deve ser **date**, contendo a data de validade do produto.* <br />
**numeroSerie:** *O campo deve ser **varchar(50)**, contendo o numero de serie do produto.* <br /><br />

> ### View de filial WMS_FILIAL

``` 
CREATE VIEW WMS_FILIAL AS 
SELECT 
codFilialErp,
nomeFilial,
nomeFantasia,
cnpj,
ativo,
codCidadeIbge
FROM FILIAL
```

**codFilialErp:** *O campo deve ser **varchar(100)** contendo o codigo da filial esse campo e chave primaria e **obrigatorio**.* <br />
**nomeFilial:** *O campo deve ser **varchar(50)** contendo o nome da filial o campo e **obrigatorio**.* <br />
**nomeFantasia:** *O campo deve ser **varchar(50)** contendo a fantasia da filial o campo e **obrigatorio**.* <br />
**cnpj:** *O campo deve ser **varchar(17)**, contendo o cnpj da filial o campo e **obrigatorio**.* <br />
**ativo:** *O campo deve ser **inteiro**, contendo 1 para ativo e 0 para inativo o campo e **obrigatorio**.* <br />
**codCidadeIbge:** *O campo deve ser **inteiro**, contendo o codigo da cidadeIbge.* <br /><br />

> ### View de fornecedor WMS_FORNECEDOR

``` 
CREATE VIEW WMS_FORNECEDOR AS 
SELECT 
codFornecedorErp,
nomeFornecedor,
nomeFantasia,
tipo,
cnpjcpf,
endereco,
numEndereco,
bairro,
codCidadeIbge,
cep
FROM FORNECEDOR
```

**codFornecedorErp:** *O campo deve ser **varchar(20)**, contendo o codigo do fornecedor esse campo e chave primaria e **obrigatorio**.* <br />
**nomeFornecedor:** *O campo deve ser **varchar(60)** contendo a razão social do fornecedor o campo e **obrigatorio**.* <br />
**nomeFantasia:** *O campo deve ser **varchar(50)** contendo o nome fantasia do fornecedor o campo e **obrigatorio**.* <br />
**tipo:** *O campo deve ser **inteiro** contendo 0 para pessoa fisica e 1 para pessoa juridica o campo e **obrigatorio**.* <br />
**cpfCnpj:** *O campo deve ser **varchar(14)** contendo a inscrição da pessoa fisica ou juridica o campo e **obrigatorio**.* <br />
**endereco:** *O campo deve ser **varchar(60)** contendo o endereço do fornecedor.* <br />
**numEndereco:** *O campo deve ser **varchar(10)** contendo o numero do endereço do fornecedor.* <br />
**bairro:** *O campo deve ser **varchar(30)** contendo a descrição do bairro do fornecedor.* <br />
**codCidadeIBGE:** *O campo deve ser **inteiro**, o mesmo e chave primaria o campo e **obrigatorio**.* <br />
**cep:** *O campo deve ser **varchar(8)** contendo o contendo o codigo postal do fornecedor.* <br /><br />


> ### View de funcionario WMS_FUNCIONARIO

``` 
CREATE VIEW WMS_FUNCIONARIO AS 
SELECT 
codFuncionarioErp,
nomefuncionario,
ativo
FROM FUNCIONARIO
```

**codFuncionarioErp:** *O campo deve ser  **varchar(20)**, contendo o codigo do funcionario esse campo e chave primaria e **obrigatorio**.* <br />
**nomefuncionario:** *O campo deve ser **varchar(60)** contendo o nome do funcionario o campo e **obrigatorio**.* <br />
**ativo:** *O campo deve ser **inteiro** contendo 0 para inativo e 1 para ativo o campo e **obrigatorio**.* <br /><br />