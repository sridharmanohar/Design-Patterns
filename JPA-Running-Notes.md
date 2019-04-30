## Query creation using Spring Data Repositories
1. This allows us to query db by just mentioning the method names which have to follow a certain nomenclature.
2. For e.g. For the entity User having properties firstname, lastname, username, password, doj etc.
3. If you want to query a user/list of users on the basis of their firstname then simply create an interface by extending the Repository interface (pass in the entity name along with its primary key type).
4. And, then write a method as : User findByUsername(String name).
5. The prefix's like findBy, readBy, queryBy, countBy, getBy will be stripped by Spring and then it will look for a field by the name username in the entity (case matters).
6. If in the above case, you mention, findByUserName then Spring will look for a field naming userName in the entity.
7. Many keywords like And, Or etc are also supported. For complete list look at Spring Data JPA ref. doc.

## @Query
1. This belongs to spring data jpa.
2. This allows us to mention the query ourself still using object domain model.
3. Alternatively, if you want to mention a native sql query then you can use the nativeQuery=true attr of this annot. and mention the query in native sql.

## @Entity
1. This is a JPA annotation.
2. Basically means a class can be mapped to a table.

## @GeneratedValue
1. This is a JPA annot.
2. When using mysql always use IDENTITY as your generation strategy because in mysql there is no direct concept of sequences  (mysql has auto_increment), so because of which when you set it to AUTO it looks for the hibernate_sequence which it
will not find and throw an error, hence use IDENTITY.

## @Column
1. If the name of the field/property in your bean is in camelCase then Spring will automatically convert that into snake_case.
2. And, if you db col name is not in snake_case then there will be an obvious mismatch and an error will be thrown during
query execution.
3. To avoid this, you can use the name attr of the annot. and specify the name that you want spring to use.

## @Size
1. You can use this annot. to specify the min/max size of the field and spring will take care of the validations.

## @NotNull
1. Valid as long as it is not null, but can be empty.

## @NotEmpty
1. Valid as long as it is not null and size/length is greater than zero.

## @Transient
1. If you do not want to persist any field of an entity then use this annot. to tell JPA that this particular should not
be persisted.

## @ManyToMany
1. This belongs to javax persistence (jpa) package.
2. In hibernate, by default, whenever you are trying to load a collection the fetch type is set to LAZY and this will lead to an error if you are not using hibernate session (spring uses EntityManager of its own).
3. So when not using hibernate sessions w/ spring and if you have collections in your entities then explicitly set the fetchtype to eager.
5. This is an attr. of this annot.

## @JoinTable
1. This is also part of jpa (javax persistence).
2. This is for letting your jpa provider know which join tables to look for while querying for data.
3. That is, say, you have 2 entities: Employee (mapped to EMPLOYEE table) and Projects (mapped to PROJECTS tab.) and then there is a third table EMPLOYEE_PROJECTS (which contains pk's of EMPLOYEE and PROJECTS tab.), and this third table is not an entity, so to let your jpa provider of this third impo. tab. which is not an entity in your app, use @JoinTable and its attrs.

## Spring Data
1. This is one of the projects in Spring family and this is an umbrella project.
2. The main purpose of this is to make it easy to access different relataion, non-relational databases, map reduce frmaeworks and cloud-based data services.
3. This umbrella project contains many sub-projects related to specific db.
4. Some of the sub-projects under this are Spring Data JDBC, Spring Data LDAP, Spring Data MongoDB etc.

## Spring Data JPA
1. This is a sub-project under the Spring Data project.
2. This is kind of a library which helps dealing with JPA easier.
3. Some of its features are pagination support, @Query annot. etc.
4. You still have to use an JPA implementation like hibernate even when using Spring Data JPA.

## MultipleBagFetchException
1. You encounter this when one or more of entities have more than one collection association.
2. Say, an entity User has two collections being loaded with @OneToMany and @ManyToMany (two Lists<>), then hibernate throws this exception.
3. This can be avoided in the following ways:
4. Convert one of the List's to a Set implementation. Of course, this approach has its own disadvantages. If you are particular on the insertion order and if you want to do index based operations then this approach is not for you.  
5. Second option is to, use Subselect as FetchMode on one of the collections. But, this will have performance implications as hibernate will have to fetch this using subqueries. Not a very preferrred option.
6. The third option is to use FetchType as LAZY, but then hibernate will throw a LazyInitializationException when you do this, and in order to overcome that you need to annotate the method which accesses this collection with @Transactional.
7. The @Transaction annot. can be of the javax.persistence package or a spring annot.

## Things to take care while doing DDL (insert, update, delete)
1. You need to make sure the method (performing the ddl) is annotated with @Transactional and @Modifying annot.
2. @Transactional can be done at class level also but @Modifying is method level.
3. @Transactional is available in both jpa api and spring transaction api. You can use any.
4. @Modifying is in springs data jpa.
5. If you don't use these you'll get errors like:
org.hibernate.hql.internal.QueryExecutionRequestException: Not supported for DML operations
Executing an update/delete query; nested exception is javax.persistence.TransactionRequiredException
6. Btw, these are only required if you are either using a jpa query or a native sql query. Not required when using spring data jpa.

## Cascade ALL
1. If you do not use this, then cascading updates/insertions will not happen.

## @Valid
1. Part of JPA validation package.
2. This enables the validations done by using JPA annot. such as @NotNull, @Size, @NotEmpty on the pojos to be available in the front-end like thymeleaf.
3. Say, if there is a empty validation violation, then the error message that is generated is passwd back to the view for it access and display it on the screen.
4. If you do not use this, validation will still happen but the error message wont appear on the screen and hence the transaction fails with the stack trace.
5. This is useful only when you are using the jpa validation annot.

