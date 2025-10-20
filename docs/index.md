# Template de Entrega


???+ info inline end "Edição"

    2025.5


## Aluno

1. Vitor Raia

## Entregas

- [x] Roteiro 1 - Data 24/09/2025
- [x] Roteiro 2 - Data 07/10/2025
- [x] Roteiro 3 - Data 15/10/2025
- [x] Roteiro 4 - Data 17/10/2025
- [ ] Projeto

## Diagrama

``` mermaid
flowchart LR
    subgraph api [Subnet API]
        direction TB
        gateway --> account
        gateway --> auth:::red
        gateway --> product
        gateway --> order
        gateway --> exchange
        auth --> account
        order --> product
        account --> db@{ shape: cyl, label: "Database" }
        product --> db
        order --> db
    end
    exchange e3@==> 3partyapi:::green@{label: "3rd-party API"}
    internet e2@==> |request| gateway:::orange
    e2@{ animate: true }
    e3@{ animate: true }
    classDef green fill:#cfc
    classDef orange fill:#FCBE3E
```

## Códigos

=== "De um arquivo remoto"

    ``` { .yaml .copy .select linenums='1' title="main.yaml" }
    --8<-- "https://raw.githubusercontent.com/hsandmann/documentation.template/refs/heads/main/.github/workflows/main.yaml"
    ```

=== "Anotações no código"

    ``` { .yaml title="compose.yaml" }
    name: app

        db:
            image: postgres:17
            environment:
                POSTGRES_DB: ${POSTGRES_DB:-projeto} # (1)!
                POSTGRES_USER: ${POSTGRES_USER:-projeto}
                POSTGRES_PASSWORD: ${POSTGRES_PASSWORD:-projeto}
            ports:
                - 5432:5432 #(2)!
    ```

    1.  Caso a variável de ambiente `POSTGRES_DB` não exista ou seja nula - não seja definida no arquivo `.env` - o valor padrão será `projeto`. Vide [documentação](https://docs.docker.com/reference/compose-file/interpolation/){target='_blank'}.

    2. Aqui é feito um túnel da porta 5432 do container do banco de dados para a porta 5432 do host (no caso localhost). Em um ambiente de produção, essa porta não deve ser exposta, pois ninguém de fora do compose deveria acessar o banco de dados diretamente.


## Exemplo de vídeo

Lorem ipsum dolor sit amet

<iframe width="100%" height="470" src="https://www.youtube.com/embed/3574AYQml8w" allowfullscreen></iframe>


## Referências

[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/reference/){:target='_blank'}