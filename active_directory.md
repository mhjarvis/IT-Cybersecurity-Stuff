# Active Directory

A `Windows Domain` allows us to overcome the problem that arises with lots of computers and users spread out over an area that needs to be managed/administered. The idea is to administer all of these components under a single repository, or `Active Directory (AD)`. The server running the AD is known as the `Domain Controller (DC)`. This provides two important advantages, `centralized identity management` meaning all users on a network can be configured from AD with minimum effort, and `managing security policies`, meaning they can be configured directly from AD and applied to users and computers across the network as needed.

The `Active Directory Domain Service (AD DS)` acts as a catalogue that holds the information of all the 'objects' that exist on the network (e.g. users, printers, groups, machines, etc).

`Users` are known as `security principals`, meaning they can be authenticated and assigned privilegas over `resources` like files or printers. They can be used to represent both people and services (e.g. IIS or MSSQL). Every service requires a user to run, but they will be limited in the priviligies as they only need that which allows them to run their specific service.

`Machines` are another object and considered a security principal. Machine account names are usually the computer's name followed by a dollar sign (e.g. DC01$).

`Security Groups` are user groups which you can assign rights / resources to and apply to all users. These are also considered security principals. Groups can have both users and machines as members, along with other groups.

`Organizational Units` are container objects that allow you to classify users and machines. They are used to define sets of users with similar policing requirements.
