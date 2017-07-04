# POST and PUT

A question for every REST developer which is often left unanswered - When do you use POST and/or PUT? What is the difference between the two? When asked to a front-end engineer, most answers have one common thing - **If REST is about CRUD operations, then POST and PUT are equivalent to Create and Update**. That clearly is not the case. Clearly, front-end engineers do not design/develop REST API, but it should hardly be an excuse to get away with a faulty understanding. After all, they are the consumers of API, if they don't question the validity of design, who will? During technical discussions and interviews, I tried to find out cause for this common misunderstanding. Findings are interesting. Front-end developers never really bother about learning REST. They only see list of API and their request/response JSON data. Ideas of HATEOAS are way distant dream. We have this tendency to believe commonly occuring patterns as facts and as such at many places above assumption about POST for creation and PUT for update holds true. Nevertheless, we shall try to distill our understanding.

There are two governing laws when it comes to choose between POST and PUT

1. **Resource idempotence**
2. **Resource location**

## Resource idempotence

> An operation \(one of the CRUD\) associated with a REST resource is considered idempotent if multiple invocations of that operation produce the same result.

In other words, if we make a same API call multiple times, then it produces same result. For example:

```
PUT /users/123/picture/456        ==>    204 No Content
```

PUT call tries to update user's profile picture. If we execute same API with same picture \(i.e. same request body\) multiple times, then nothing will happen on subsequent calls. Whatever observable thing, updating user profile picture in this case, should have happened on first API call. Subsequent API calls will just overwrite it with same data or simply ignore API. It is not creating any more side effects. This is called as idempotency of an operation.

Now, consider another example:

```
POST /accounts/123/transaction    { withdrawal: 20 }        ==>     202 Accepted
```

POST call tries to create a transaction resource on account 123. Here we are trying to create withdrawal type of transaction with amount of $20. So if account 123 has $100, then first API call will change the balance to $80. If I make exactly same API call one more time \(absolutely changing nothing\), then account balance will come down to $60. It means by fifth time, account balance would have completely exhausted. So here, **each subsequent identical request to a resource produces unique side-effect. This is called as non-idempotent operation**.

As you might have guessed, we should try to model our operations idempotent and thus prefer PUT wherever we can. Advantages are obvious: Idempotent operations are safe making system more resilient and test friendly. And, use POST whenever we need to perform non-idempotent operation.

Bottom-line: **PUT for idempotent \(safe\) and POST for non-idempotent**

## Resource location

In RESTful systems, resources are identified by their unique address \(URI or on web URL\). So no matter:

> If you know the exact location of your resource, then you should **use PUT to create or update** a resource subject to laws of idempotency. Otherwise, use POST.

We use databases to persist our resources. Often, a primary key serves as a unique address for that resource. Traditionally, primary key is database table's auto increment column and hence generating unique key for a resource is made part of database. It is difficult to pass custom values to this column from code. Direct implication of this is that a client making an API call can probably never get rights to choose its own location to create resource.

But with advent of UUID/GUID, it is now possible to generate random unique key anywhere and feed it to database. Read more about the uniqueness of UUID [here](https://stackoverflow.com/questions/1155008/how-unique-is-uuid "How unique is UUID?"). For example:

```
PUT /candidates/19bf2c79-6feb-4344-bbe3-565c24e09b0b    { name: 'HP', ... }
==>    201 Created
```

Here we are trying to create new candidate resource and it is the client who has provided where to put this resource \(19bf2c79-6feb-4344-bbe3-565c24e09b0b\). Or if client lacks ability to generate UUID then it can still:

```
POST /candidates/    { name: 'HP', ... }    ==>    201 Created
```

And it should just work fine. Having said this, you should expose something like `PUT /candidates/19bf2c79-6feb-4344-bbe3-565c24e09b0b` only if it is safe and idempotent. By exposing such API, I am telling API consumers that creating a candidate is safe operation. So if you fire request multiple times, there is no problem. In real world, that may not be the case. Example here is purely fictional. Remember the last condition: **Subject to laws of Idempotency**.

## Conclusion

Someone had asked me: what if I expose `PUT /candidates/19bf2c79-6feb-4344-bbe3-565c24e09b0b`. Should I throw error \(403\) or overwrite \(204\) or create \(201\) on multiple request? It means you are still missing the point of the above paragraph. **Some people have opinion that PUT should have either create or update semantic.** If resource exists then just do update or create if it doesn't. I believe meanings should be explicit and hence such double behavior depending upon context should be avoided. But I have seen some scenarios where this create or update using PUT is useful. One scenario is caching search result. If your search query is very complex, you can store that query in database for future use. So if you use PUT to manage this **SearchQuery** resource, then on first attempt you will create it \(HTTP 201\). Storing SearchQuery is idempotent. If you then modify it and since you know exact location, you can simply use PUT again to update it.

Below is the simple table that will help you choose right method:

| Idempotent | Location | Method |
| :--- | :--- | :--- |
| Yes | Yes | PUT |
| Yes | No | POST \(Or PUT if dealing with **SearchQuery** like resource\) |
| No | Yes | POST |
| No  | No | POST |

Finally, one last traditional scenario where you might need to use **POST**? When you are trying to filter extremely large dataset with lots of options and filter settings. You would use **GET**. But it is probably not possible due to size of URL string. Old time servers/routers had limit of 255 character in a query. Maybe when you come across such scenario, you might want to tweak RESTful ideas to suit your needs.

### Exercise:

1. What method should be used to change user password?
2. How will you fit Facebook's GraphQL in this description?
3. How caching plays the role in POST and PUT?



