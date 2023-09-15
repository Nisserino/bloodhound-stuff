# Bloodhound-stuff
*tips/tricks/caveats and queries*

[install instructions](install_instructions.md)  
[how to get data](how_to_sharphound.md)  
[Neo4j queries](queries.md)  
[bloodhound tips](bloodhound_tips.md)  

## Caveats/help wanted
- This guide is assuming the host running bloodhound will be a parrot or kali installation. Only parrot has been tested, and a test-run on windows will not be tested at all unless someone other than me does it (: *probably won't try to do it on kali either, but shouldn't be a problem as parrot has the same base*

- Automating import of sharphound data  
    There is currently no intended way to automatically populate the neo4j database.  
    [link to issue/request for feature](https://github.com/BloodHoundAD/BloodHound/issues/248)

- Neo4j is too old (most of the times) in the standard repos.  
    this is fixed by installing neo4j from their repos, not hard, but an extra step.

- Bloodhound won't tell you the contents of GPOs, but will show you where they are linked  
    You'll also be able to see who can modify a gpo.

- Importing a session loop scan will take a shitload of time
    - the scan will run for two hours, and create a zip every 5 mins
    - after two hours, it will (by default) stop, and package all generated zips into a larger one.
    - You'll have to unpack the zip-zip so that you can drag-and-drop the shitload of smaller zips