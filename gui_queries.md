# Queries to be used in the GUI

### Domain Controller object ownership.
- Bad if Domain Admins is not the owner
     - Classical misconfig is that a user (likely techician) is the owner. 
        - Good sign that there is a routine missing for handling ownership.
```
MATCH (g:Group)
WHERE g.objectid ENDS WITH '-516'
MATCH p = (n:Base)-[:Owns]->(c:Computer)-[:MemberOf*1..]->(g)
RETURN p
```

### Privileged kerberoastable users
```
MATCH p = shortestPath((u:User {hasspn:true})-[*1..]->(g:Group))
WHERE g.objectid ENDS WITH '-512'
RETURN p
```

### Domain Users group and other large groups having control of other objects 
```
MATCH p = (g:Group)-[{isacl:true}]->(m)
WHERE g.objectid ENDS WITH '-513'
RETURN p
```

### Privileged null nodes
*a "null node" in bloodhound, is a node (object) in the domani that is only represented by a SID.*  
*Usually this is due to the object belonging to a trusted domain, or the ojbect has been removed from the domain, but is still referenced in existing objects ACLs*
> To ascertain which of the above YOUR null node is, check the SID and see if it matches your domain. If it does, it's a deleted object, if not, it's from a trusted domain.
```
MATCH (x) WHERE x.distinguishedname is null MATCH p=(x)-[r]->() RETURN p
```

### Orphaned groups
Groups without members or memberships
```
MATCH (p:Group) WHERE NOT ()-[:MemberOf]->(p) AND NOT (p)-[:MemberOf]->() RETURN p
```