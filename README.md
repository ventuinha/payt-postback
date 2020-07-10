Documentação de Postback PayT
-----------------------------

Por agora são apenas exemplos que se encontram na pasta do projeto.

  

  

### Fluxos de Atividade

é possível perceber um fluxo de atividade do cliente através do `cart_id`

resumidamente temos 4 fluxos nos exemplos, recomendo utilizar eles para ir em ordem cronológica

  

1.  Cartão de Crédito falha e sucesso
    1.  [Falha](https://github.com/ventuinha/payt-postback/blob/master/examples/cancelled.md)
    2.  [Sucesso](https://github.com/ventuinha/payt-postback/blob/master/examples/credit_card.md)
2.  [Boleto](https://github.com/ventuinha/payt-postback/blob/master/examples/bankslip.md)
3.  Compra com utm\_source e src + upsell
    1.  [Cartão de crédito com utm\_source](https://github.com/ventuinha/payt-postback/blob/master/examples/with_utm_sources.md)
    2.  [Upsell](https://github.com/ventuinha/payt-postback/blob/master/examples/upsell.md)
4.  Carrinho abandonado + compra recuperada + upsell manual
    1.  [Carrinho abandonado](https://github.com/ventuinha/payt-postback/blob/master/examples/lost_cart.md)
    2.  [Compra](https://github.com/ventuinha/payt-postback/blob/master/examples/cart_recovered.md)
    3.  [Upsell manual](https://github.com/ventuinha/payt-postback/blob/master/examples/manual_upsell.md)