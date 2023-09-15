# Custom Queries
## How to add custom queries
### Classic free bloodhound
On linux, the custom queries shown in the GUI can be populated by modifying the file below   
```bash
~/.config/bloodhound/customqueries.json
```  

*example query*  
```json
{
        "queries": [
                {
                        "name": "testQ",
                        "category": "TestCategory",
                        "queryList": [
                                {
                                        "final": true,
                                        "query": "match (u:User) where u.admincount = true return u",
                                        "allowCollapse": true
                                }
                        ]
                }
        ]
}
```  

### Bloodhound CE 
iunno