# Understanding second level cache in hibernate using Ehcache

#Introduction : 

The second level cache is responsible for caching objects across sessions. When this is turned on, objects will
first be searched  in the session if it not found then delegates searching in the cache and if they are not found,
a database query will be fired. Second level cache will be used when the objects are loaded using their primary key.
This includes fetching of associations. Second level cache objects are constructed and reside in different memory locations.

#How Second level cache works in hibernate ? 

When ever hibernate session try to load an entity, the very first place it look for cached copy of entity
in first level cache (i,e hibernate session).If cached copy of entity is present in first level, it is returned
as result of load method.If there is no cached entity in first level cache, then second level cache is looked up
for cached entity.If second level cache has cached entity, it is returned as result of load method.
But, before returning the entity, it is stored in first level cache also so that next invocation to load method
for entity will return the entity from first level cache itself, and there will not be need to go to second level
cache again.If entity is not found in first level cache and second level cache also, then database query is executed
and entity is stored in both cache levels, before returning as response of load() method.Second level cache validate
itself for modified entities, if modification has been done through hibernate session APIs.

Here is the [Blog](http://akorsa.ru/?p=5446&preview=true) of this project with precise explanation.
