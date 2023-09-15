# installation & setup
## Table of contents
1. [Neo4j](##Neo4j) 
    - [installation](###Neo4j-installation)
    - [setup](###Neo4j-setup)
    - [caveats](###Caveats)
2. [Bloodhound](##Bloodhound)
    - [installation](###Bloodhound-installation)
    - [setup](###Bloodhound-setup)
## Neo4j
*debian install, installing from their repo is a must, as default repo neo4j is too old for bloodhound*  
*This will work on parrot/linux that are up to date, persuming you haven't messed with java installations*  
### Neo4j installation
1. Add neo4j repo 
    ```bash
    wget -O - https://debian.neo4j.com/neotechnology.gpg.key | sudo apt-key add -
    echo 'deb https://debian.neo4j.com stable latest' | sudo tee -a /etc/apt/sources.list.d/neo4j.list
    sudo apt-get update
    ```

2. list the available neo4j versions.  
    ```bash
    apt list -a neo4j
    # Listing... Done
    # neo4j/stable,now 1:5.1.0 all 
    # neo4j/parrot,parrot 4.2.1-0parrot1 all

    ```  
3. Install the latest available version 
    ```bash
    # in the above case, the lateste version was 1:5.1.0
    # use the highest version neo4j/stable lists
    sudo apt install neo4j=1:5.1.0
    ```

### Neo4j setup
1. Start neo4j in console mode  
    ```bash
    sudo neo4j console
    ```  
2. open a browser and go to "localhost:7474" and log in user: neo4j password: neo4j
    >You will be forced to set a new password after first login.

3. After neo4j has been set up, you can start neo4j with the command:
    ```bash
    sudo neo4j start
    ```

### Caveats
- Java version problems
> Neo4j uses java 11, so if you don't have it on your system, it needs to be installed.
To set java11 as the default, run sudo update-alternatives --config java and select java11 from the list.
it has a number on lefthand side in the list and press enter

*note that it should not be a problem on debian kali/parrot*
## Bloodhound


### Bloodhound installation

Start Bloodhound ./<path-to-bloodhound>
    log in using the credentials set in neo4j

Import graphs from sharphound run
    drag and drop the zip sharphound generated or
    unzip the sharphound zip and then drag-and-drop all <somename>.json into bloodhound

### Bloodhound setup