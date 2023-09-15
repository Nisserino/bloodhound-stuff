# Some nice to have queries
These queries are mainly intended to be used in the neo4j web-console, 
but with some modification to the return values it can be used in bloodhound gui aswell

### Good to have snippets

#### convert epochseconds to something useful
> Replace `<DATE>` with the thing you want a proper date on (ie User.pwdlastset)
```
datetime({epochSeconds:toInteger(<DATE>)})
```

### General
#### Find unsupported OSs
> Returns csv with unsupported os, sorted by enabled, disabled computers first.
```
MATCH (H:Computer) WHERE H.operatingsystem =~ '.*(2000|2003|2008|xp|vista|7|me).*' 
RETURN H.name as Computer, H.operatingsystem as OS, H.enabled as Enabled order by Enabled
```

#### Find kerbrostable accounts with password set more than a year ago
> If a user has spn, it's kerbroastable (it's a service account), if it's not enabled, it's a bit more safe  
but it should be removed as quickly as possible.  
the krbtgt should have a rotating password policy to avoid getting golden ticketed 
```
MATCH (u:User) WHERE u.hasspn=true AND u.pwdlastset < (datetime().epochseconds - (60 * 60 * 24 * 356)) 
RETURN u.name as User, datetime({epochSeconds:toInteger(u.pwdlastset)}) as Password_last_set, u.enabled as enabled order by u.pwdlastset
```

#### list disabled users and order by lastLogon
> if there are a lot of disabled accounts that hasn't been logged into for a year, it's a good sign that there isn't a policy for account removal when there probably should be.
```
match (u:User) where u.enabled = false
return datetime({epochSeconds:toInteger(u.lastlogon)}) as lastLogon, u.name order by lastLogon
```

#### List accounts with 'adminCount' that have an SPN
> Obvious "aja-baja", will contain very few 'false positives', but might leave out a couple of true positives if a user isn't a proper admin, but has admin-like rights or has rights enough to get too high privs.
```
match (u:User) where u.enabled = true and u.admincount = true and u.hasspn = true 
return u.name
```
### Low hanging fruit
#### Users which might have password in description  
```
MATCH (u:User) WHERE toUpper(u.description) CONTAINS 'PASS' RETURN u.name,u.description
```
