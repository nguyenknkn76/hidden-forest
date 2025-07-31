1. theory about db
2. sql from basics to advances
3. db nomalization
4. advances operation of database
5. applications: connect proj to database

# INTRO
**compare db with exel**
**compare dbms with file system**
## Some concepts
**Database**
**Database management system(DBMS)**: posgresql, mysql
- advanced problems: access control(authorization), redis
- applications
- disadvantages
- components of dbms

**abtract model: 3 layers** → dbms: data independence
- view layer
- logic layer → focus this one
- phyical layer 

**architect**: 2 layer(client-server), 3 layer(client-server-db)

- data modeling: real obj → db(table,...)
- design db

**entity relationship diagram** 
- 3 comps: entities, relationship, properties
- symbols
- types of entities: strong entity(have primary key), weak entity
- types of properties: single(atomic)-multi,...
- quantity reltionship mapping 
- key: primary key < candidate key < super key (many properties) → `SHOULD BE NUMERIC`

## Some problem in design er diagram
**quantity relationship mapping**
- `n-n`
- `1-n`
- `1-1`

**parent class && class**:
- class inherits properties and relationship from parents
- specialization: can define class from parent class (by using property of parent)
- generalization

> someproblem: 
> - deadlock
> - meta data

# My process: 2/25