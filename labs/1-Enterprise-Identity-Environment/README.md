# Enterprise Identity Lifecycle
### Building the Foundation of Enterprise Identity

This implementation establishes the foundation of an enterprise identity environment. Beginning with Active Directory, we'll establish a directory integration with Okta, configure identity sourcing, synchronize user attributes, and automate access through group-based assignments before moving into authentication, federation, and lifecycle management.

To properly simulate a directory integration/multiple profile sources (that’ll exist in an enterprise environment), we begin with a Windows Server, to install Active Directory.

<img src="YOUR_IMGUR_LINK_HERE_1" alt="Windows Server">

<br>

Within the (empty) server, add ‘Active Directory Domain Services’ as one of its feature.

<img src="YOUR_IMGUR_LINK_HERE_2" alt="Active Directory Domain Services">

<br>

Then, promote the server (i.e. make responsible for managing Active Directory) to a Domain Controller.

<img src="YOUR_IMGUR_LINK_HERE_3" alt="Domain Controller">

<br>

Users are one of the many objects within Active Directory. ‘User 2’ is now part of the forest/domain ‘dev-ad.com’.

<img src="YOUR_IMGUR_LINK_HERE_4" alt="Active Directory Users">

<br>

In order for users within a directory to synchronize to Okta (i.e. IAM Platform) there must be a connector. The connector is then installed on the Windows Server, with Active Directory. The ‘Okta AD Agent’ makes outbound calls to the internet (i.e. Okta) and pushes/imports directory changes (i.e. new users, groups, etc.).

<img src="YOUR_IMGUR_LINK_HERE_5" alt="Okta AD Agent">

<br>

After successful integration, Active Directory now becomes an official profile source.

<img src="YOUR_IMGUR_LINK_HERE_6" alt="Active Directory Profile Source">

<br>

One of the configurations to note is ‘Profile & Lifecycle Sourcing’, if checked, AD owns the user. A user is a collection of attributes. Meaning, those attributes (for AD originated users) can not be edited within Okta.

<img src="YOUR_IMGUR_LINK_HERE_7" alt="Profile & Lifecycle Sourcing">

<br>

The Universal Directory is a collection of users. Every integrated user becomes an Okta user.

<img src="YOUR_IMGUR_LINK_HERE_8" alt="Universal Directory">

<br>

Again, a user is a collection of attributes. Certain attributes already exist within a directory, for example, ‘badPwdCount’. To pull data from a source attribute (i.e. originated attribute) to a destination attribute (i.e. another profile source like Okta) is called Attribute Mapping. Only ‘map’ relevant data/attributes (that’ll contribute to downstream applications).

<img src="YOUR_IMGUR_LINK_HERE_9" alt="Attribute Mapping">

<br>

Because AD owns this user (i.e. an AD user), inheriting its value from AD, the attribute cannot be edited from Okta.

<img src="YOUR_IMGUR_LINK_HERE_10" alt="Read-only Attribute">

<br>

Attribute level mastering (ALM) is the act of specifying the profile source that owns the singular attribute. Here, the source priority becomes Okta.

<img src="YOUR_IMGUR_LINK_HERE_11" alt="Attribute Level Mastering">

<br>

Since the source priority changed, its now editable from Okta. However, on AD its still ‘editable’ but because Okta is now the owner of this attribute, it’ll ignore whatever the value is on AD, and only respects the value from Okta.

<img src="YOUR_IMGUR_LINK_HERE_12" alt="Okta Attribute Owner">

<br>

Now, there are 5 groups within this enterprise. The custom groups are: IAM Engineering, IT Help Desk and HR.

<img src="YOUR_IMGUR_LINK_HERE_13" alt="Groups">

<br>

‘Certs’ is a custom attribute, created in Profile Editor. This attribute is a string array with enumerated values (which is preferred since it evaluates nicer than a regular string).

User 5 has both Okta Certified Professional and Okta Certified Admin cert.

<img src="YOUR_IMGUR_LINK_HERE_14" alt="Custom Attribute">

<br>

Now, a group rule is an automated means for group membership. Okta’s Identity Engine is responsible for evaluating the environment surrounding its users. Because it’s a string array, Okta’s EL is written as `Arrays.contains(user._, _)`. This group rule automatically adds users with both certs to the ‘IAM Engineering’ group.

<img src="YOUR_IMGUR_LINK_HERE_15" alt="IAM Engineering Group Rule">

<br>

This is the group rule for ‘IT Help Desk’. It states that users with either ‘Monica’ as their manager or are interns, will be automatically added.

<img src="YOUR_IMGUR_LINK_HERE_16" alt="IT Help Desk Group Rule">

<br>

The results of the Identity Engine evaluating the environment (i.e. group rules).

<img src="YOUR_IMGUR_LINK_HERE_17" alt="Group Rule Results">
