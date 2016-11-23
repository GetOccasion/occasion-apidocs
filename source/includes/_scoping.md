# Merchant Scoping

If you are using the Occasion API to access your own merchant's resources, you can skip this section. If you are an Occasion partner using the Occasion API to access other merchants' resources, this section is relevant to you.

Occasion partners are issued credentials that require them to specify a merchant scope when making requests to resource indexes. What we mean by a merchant scope is: You can access all merchants, but if you want to access all products, it can only be for one merchant at a time. A few examples should clarify what we mean:

```shell
curl "http://app.getoccasion.com/api/v1/merchants"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

> All merchants will be returned, because you have access to all of them

```shell
curl "http://app.getoccasion.com/api/v1/products?merchant_id=jsh8e0a"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

> All products belonging to merchant with id='jsh8e0a' will be returned

```shell
curl "http://app.getoccasion.com/api/v1/products"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

> 400 Bad Request will be returned because you must provide a merchant_id to scope with, you cannot access all products of all merchants at once

```shell
curl "http://app.getoccasion.com/api/v1/products/37shd72"
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

> Product with id='37shd72' will be returned. No merchant scope is required because this is a request to a specific product for a specific merchant.

```shell
curl "http://app.getoccasion.com/api/v1/products?merchant_id=jsh8e0a"
  -X POST
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

> Created product belonging to merchant with id='jsh8e0a' will be returned.

```shell
curl "http://app.getoccasion.com/api/v1/products"
  -X POST
  -u "59a8517fd9458b46d4ee59f8fd717fb80d:de7b7ae9e2e9e01a9508290e599"
```

> 400 Bad Request will be returned because the product cannot be created without a merchant scope.
