# [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)
- A software architecture style that defines **a set of constraints** to be used for **creating web services(resoures)**.
- Abbreviation of REpresentational State Transfer.

## Constraints
### Client-server architecture
![client-server model](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c9/Client-server-model.svg/500px-Client-server-model.svg.png)
- Seperation of concerns.
- Seperating the userinterface concerns from the data storage concerns improves the portability of the user inter face across multiple platforms.
- It improves scalability by simplifying the server components.
- 일관적인 인터페이스로 분리되어야 한다.

### Statelessness
- The client-server communication is constrained by no client context being stored on the server between requests.
- 각 요청 간 클라이언트의 컨텍스트가 서버에 저장(maintain)하지 않는다.

### Cacheable
![cache](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a1/Cache_Coherency_Generic.png/400px-Cache_Coherency_Generic.png)
- Clients and intermediaries can cache responses.

### Layered System
- A client cannot ordinarily tell whether it is connected directly to the end server, or to an intermediary along the way.

### Uniform Interface
- fundemental to the design of any REST service.
- URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일

### Code on demand(optional)
- Servers can temporarily extend or customize the functionality of a client by transferring executable code.
- For example, server offers javascript.

## Guides
### Resource identification in requests
- Individual resources are identified in requests.
```
GET http://www.resources.com/items/17
```

### Resource manipulation through representations(messages)
- When a client holds a representation of a resource, including any metadata attached, it has enough information to modigy or delete the resource.
```
POST http://www.resources.com/items
{
  item_name: "blahblah"
}
```
### Self-descriptive message
- REST 메세지만 보고도 쉽게 이해할 수 있는 자체 표현 구조로 구성.
```
GET http://www.resources.com/items/17
```
### Hypermedia as the engine of application state
- Hypermedia: extension of hypertext including sounds, or other media.
- 클라이언트가 관련된 리소스에 접근하기를 원한다면, 리턴되는 지시사에서 구별될 수 있어야 한다.


## RESTful API
- based on [CRUD(Create, Read, Update, Delete)](https://ko.wikipedia.org/wiki/CRUD)

| 구분 | 표현 |
|----|------|
|Resource| URI|
|Verb| HTTP Method(GET, PUT, POST, DELETE, PATCH)|
|Representations|data|


### Create
- Create a resource
```
POST http://www.resources.com/items
{ data : ... }
```

### Read
#### Index
- Get list of resources.
```
# GOOD
GET http://www.resources.com/items

# BAD
GET http://www.resources.com/items/list
```

#### Show
- Show a resource.
```
# GOOD
GET http://www.resources.com/items/17

# BAD
GET http://www.resources.com/items/show/17
```

### Update
- Update a resource of all
```
PUT http://www.resources.com/items/17
{ data : ... }
```

- Update a part of a resource
```
PATCH http://www.resources.com/items/17
{ data : ... }
```

### Delete
- Delete a resource
```
DELETE http://www.resources.com/items/17
```

## Practice
|HTTP Verb | Path | Meaning |
|---------|------|----------|
| GET | /users | ? |
| GET | /users/new | ? |
| POST | /users |  ? |
| GET | /users/:id | ? |
| GET | /users/:id/edit | ? |
| PUT | /users/:id | ? |
| DELETE | /users/:id | ? |

<hr/>
## See also,
- https://guides.rorlab.org/routing.html
- https://spoqa.github.io/2012/02/27/rest-introduction.html
