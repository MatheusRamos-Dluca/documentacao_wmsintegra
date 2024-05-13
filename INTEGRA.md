# WMSExpert Integra
**Documentação de integração WMSExpert**

> Em todo campo de um <strong>JSON</strong> que apresentar antes dos dois pontos (:) o ponto de interrogação (?) significará que o campo não é obrigatório ser passado.

> Os campos <strong>page</strong> e <strong>size</strong> sempre que solicitados em uma requisição serão obrigatórios.

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

### Buscar Produto <br />

> O método de envio para pegar um produto específico cadastrado dentro do sistema. URL de envio e o método de envio correspondente.

```
    get: https://wmsexpert-api-55cc6cff3437.herokuapp.com/api/produto/[{idDoProdutoProcurado}]   
```

> A api retornará, caso existente, o produto na seguinte estrutura.


```
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
```


### Filtrar Produtos <br />

> O método de envio para pegar produtos cadastrados que atendam os valores dos campos passados dentro da request. Abaixo a URL de envio e o método de envio correspondente.

```
    get: https://wmsexpert-api-55cc6cff3437.herokuapp.com/produto/geral/filtro   
```

> Tipos que poderão ser passados dentro do campo sort.

```
  [ 
    "altura", 
  "unidadepadrao", 
  "subgrupo", 
  "shelflife", 
  "pesoliquido", 
  "pesobruto", 
  "nome", 
  "lastro", 
  "id", 
  "grupo", 
  "fornecedor", 
  "estoqueminimo", 
  "endereco", 
  "empresa", 
  "controlavalidade", 
  "codigo", 
  "codigoref", 
  "controlalote", 
  "controlanumserie" 
  ]
```

> A seguir os parametros a serem passados na request: 

```
    {
        page: integer,
        size: integer,
        sort?: enum,
        idproduto?: integer,
        codigo?: string,
        descricao?: string,
        idendereco?: integer       *obs: esse idendereco é associado ao produto. Portanto, não adiantará passar endereços aleatoriamentes, pois apenas trará caso exista algum produto associado. 
    }
```

> A api retornará, caso existente, os produtos na seguinte estrutura.

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

### Busca de Produto Por Embalagem

> O método de envio para pegar produtos cadastrados que atendam os valores dos campos passados dentro da request. Abaixo a URL de envio e o método de envio correspondente.

```
    get: https://wmsexpert-api-55cc6cff3437.herokuapp.com/produto/geral/consulta   
```

> Há apenas um parametro a ser passado nessa request:

```
    {
        codbarraprod: string
    }
```

> A api retornará, caso existente, os produtos na seguinte estrutura.

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


### Salvar Produto

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