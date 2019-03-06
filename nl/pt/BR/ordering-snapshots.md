---

copyright:
  years: 2014, 2019
lastupdated: "2019-02-05"

keywords:

subcollection: FileStorage

---
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}


# Solicitando capturas instantâneas

Para criar capturas instantâneas de seu volume de armazenamento, seja automaticamente ou manualmente, é necessário comprar espaço para mantê-las. É possível comprar capacidade até a sua quantia de volume de armazenamento (durante a compra de volume inicial ou posteriormente usando essas etapas).

## Determinando a quantidade de espaço de captura instantânea a ser pedido

Genericamente falando, o espaço de captura instantânea é usado por capturas instantâneas com base em dois fatores principais:
- Quanto seu sistema de arquivos ativo muda ao longo do tempo,
- Quanto tempo você planeja reter capturas instantâneas.  

A maneira de calcular a quantia de espaço necessário é **(Taxa de mudança)** x **(número de horas/dias/semanas/meses em que os dados são retidos)**.  

A primeira captura instantânea usa uma quantidade insignificante de espaço, pois é apenas uma cópia dos metadados (ponteiros) que indica os blocos do sistema de arquivos ativo.
{:note}

Um volume com várias mudanças e um período de retenção longo precisa de mais espaço do que um volume com mudança moderada e um planejamento de retenção moderado. Um exemplo para o primeiro tipo é um banco de dados com uma alta taxa de mudança. Um exemplo para o segundo tipo é um armazenamento de dados do VMware.

Se você usar 12 capturas instantâneas por hora de 500 GB de dados reais e houver 1 por cento de mudança entre cada captura instantânea, você terminará com 60 GB para capturas instantâneas.

*(Taxa de mudança de 5 GB) x (12 capturas instantâneas por hora) = (60 GB de espaço usado)*

Por outro lado, se esses 500 GB de dados reais, com 12 capturas instantâneas por hora, vissem 10 por cento de mudança a cada hora, o espaço de captura instantânea usado seria de 600 GB.

*(Taxa de mudança de 50 GB) x (12 capturas instantâneas por hora) = (600 GB de espaço usado)*

Portanto, quando você determinar quanto espaço de Captura instantânea precisará, considere a taxa de mudança atentamente. Isso influencia enormemente a quantia de espaço de captura instantânea necessária. É mais provável que um volume maior mude mais vezes. No entanto, um volume de 500 GB com 5 GB de mudança e um volume de 10 TB com 5 GB de mudança usam a mesma quantia de espaço de captura instantânea.

Além disso, para a maioria das cargas de trabalho, quanto maior for um volume, menos espaço precisará ser reservado inicialmente. É principalmente devido às eficiências de dados subjacentes e à natureza de como as capturas instantâneas funcionam no ambiente.

## Ordenando o espaço de captura instantânea por meio do console do  {{site.data.keyword.cloud_notm}}

1. Efetue login no [Console do IBM Cloud](https://{DomainName}/){:new_window} e clique no ícone de menu na parte superior esquerda. Selecione **Infraestrutura clássica**.

   Como alternativa, é possível efetuar login no [{{site.data.keyword.slportal}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/){:new_window}.
2. Acesse seu Armazenamento por meio de **Armazenamento** > **{{site.data.keyword.filestorage_short}}**.
3. Clique em **Mudar espaço de captura instantânea** no quadro Capturas instantâneas.
4. Selecione a quantidade de espaço que você precisa e o método de pagamento.
5. Clique em **Continuar**.
6. Insira qualquer código promocional que você tenha e clique em **Recalcular**. **Encargos para este pedido** e **Revisão do pedido** têm valores padrão.

   Os descontos são aplicados quando o pedido é processado.
   {:note}
7. Marque a caixa **Eu li o Contrato de Prestação de Serviços Principal e concorde com os termos contidos nele** e clique em **Fazer pedido**. Seu espaço de captura instantânea será provisionado em alguns minutos.

## Pedindo Espaço de captura instantânea por meio do SLCLI

```
# slcli file snapshot-order --help
Usage: slcli file snapshot-order [OPTIONS] VOLUME_ID

Options:
  --capacity INTEGER    Size of snapshot space to create in GB  [required]
  --tier [0.25|2|4|10]  Endurance Storage Tier (IOPS per GB) of the file
                        volume for which space is ordered [optional, and only
                        valid for endurance storage volumes]
  --upgrade             Flag to indicate that the order is an upgrade
  -h, --help            Show this message and exit.
```
