# BloodHound Tips
*Everything here needs a spell-check*

## Useful information to grab
1. On the domain node, there's the property "functionalLevel" telling you the functional level of the domain. 
    - Cypher: `match (d:Domain) return d`
2. One of the most useful ways to see how a group is affected by other entities, is going to the bottom of the node info tab, under the header "inbound control rights", and clicking the text "Transitive control rights"
    - This will show all object controllers, both through intended and abusable paths.
3. 