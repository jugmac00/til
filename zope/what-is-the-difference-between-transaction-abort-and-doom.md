# What is the difference between transaction.abort and transaction.doom?

**Zope** is using the [transaction](https://transaction.readthedocs.io/en/latest/index.html) package to manage - you guess - transactions.

More specifically, a transaction starts when Zope receives a request, and the transaction succeeds when the action triggered by the request works out.

When the action causes an exception, the transaction will be rolled back.

This means, usually you very rarely have to interfere with the transaction management manually.

Last week I was implementing a new **XML-RPC** API, which basically looks like the following code:

```
def create_company():
  try:
      validate(data)
  except ValidationError:
      # tell client about error
  else:
     company = _create_company(data)
     return company.id
```

Now, there is a problem when the API receives invalid data.

I cannot re-raise a ValueError, otherwise the XML-RPC client just receives a meaningless `500 internal server error`.

When I return an `xmlrpc.client.Fault` object, the client gets a meaningful error message, but the **transaction succeeds**.
If there is any side effect, it gets committed.
That is not what we want here.

## transaction.abort anyone?

Ok. What about adding a `transaction.abort` in the `except` block?

This also does not yield the desired result.

The changed data / side effect still gets persisted!

Wait what?

After a transaction begins, the changed objects are marked to be persisted in case of a successful transaction - so far so good...

... but the `abort` only removes the mark, but does not undo the changed data.

After the `abort` Zope automatically starts a new transaction,
and in case those objects from before get marked again,
also the changed state from before gets persisted!

## doom to the rescue

The solution is simple (once you know it).
Instead of `transaction.abort` you have to use a `transaction.doom` - the latter one really makes sure the transaction is rolled back.
