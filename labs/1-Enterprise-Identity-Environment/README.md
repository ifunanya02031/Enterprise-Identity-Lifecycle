# Enterprise Identity Lifecycle

<h2>Lab 1 - Enterprise Identity Environment</h2>

To properly simulate a directory integration/multiple profile sources (that’ll exist in an enterprise environment), we begin with a Windows Server, to install Active Directory.

<br />

<img src="https://imgur.com/OBK96Sx.png" alt="Install Active Directory"> 

<br /><br />
Within the (empty) server, add ‘Active Directory Domain Services’ as one of its feature.
<br />
<img src="https://imgur.com/ycYKpfL.png" alt="AD DS Feature">

<br /><br />

Then, promote the server (i.e. make responsible for managing Active Directory) to a Domain Controller.

<br />

<img src="https://i.imgur.com/IMAGE3.png" alt="Domain Controller">

<br /><br />

Users are one of the many objects within Active Directory. ‘User 2’ is now part of the forest/domain ‘dev-ad.com’.

<br />

<img src="https://i.imgur.com/IMAGE4.png" alt="Active Directory Users">

<br /><br />

In order for users within a directory to synchronize to Okta (i.e. IAM Platform) there must be a connector. The connector is then installed on the Windows Server, with Active Directory. The ‘Okta AD Agent’ makes outbound calls to the internet (i.e. Okta) and pushes/imports directory changes (i.e. new users, groups, etc.).

<br />

<img src="https://i.imgur.com/IMAGE5.png" alt="Okta AD Agent">

<br /><br />

After successful integration, Active Directory now becomes an official profile source.

<br />

<img src="https://i.imgur.com/IMAGE6.png" alt="Profile Source">

<br /><br />

One of the configurations to note is ‘Profile & Lifecycle Sourcing’, if checked, AD owns the user. A user is a collection of attributes. Meaning, those attributes (for AD originated users) can not be edited within Okta.

<br />

<img src="https://i.imgur.com/IMAGE7.png" alt="Profile and Lifecycle Sourcing">

<br /><br />

The Universal Directory is a collection of users. Every integrated user becomes an Okta user.

<br />

<img src="https://i.imgur.com/IMAGE8.png" alt="Universal Directory">

<br /><br />

Again, a user is a collection of attributes. Certain attributes already exist within a directory, for example, ‘badPwdCount’. To pull data from a source attribute (i.e. originated attribute) to a destination attribute (i.e. another profile source like Okta) is called Attribute Mapping. Only ‘map’ relevant data/attributes (that’ll contribute to downstream applications).

<br />

<img src="https://i.imgur.com/IMAGE9.png" alt="Attribute Mapping">

<br /><br />

Because AD owns this user (i.e. an AD user), inheriting its value from AD, the attribute cannot be edited from Okta.

Attribute level mastering (ALM) is the act of specifying the profile source that owns the singular attribute. Here, the source priority becomes Okta.

Since the source priority changed, its now editable from Okta. However, on AD its still ‘editable’ but because Okta is now the owner of this attribute, it’ll ignore whatever the value is on AD, and only respects the value from Okta.

<br />

<img src="https://i.imgur.com/IMAGE10.png" alt="Attribute Level Mastering">

<br /><br />

Now, there are 5 groups within this enterprise. The custom groups are: IAM Engineering, IT Help Desk and HR.

<br />

<img src="https://i.imgur.com/IMAGE11.png" alt="Groups">

<br /><br />

‘Certs’ is a custom attribute, created in Profile Editor. This attribute is a string array with enumerated values (which is preferred since it evaluates nicer than a regular string).

User 5 has both Okta Certified Professional and Okta Certified Admin cert.

<br />

<img src="https://i.imgur.com/IMAGE12.png" alt="Custom Attribute">

<br /><br />

Now, a group rule is an automated means for group membership. Okta’s Identity Engine is responsible for evaluating the environment surrounding its users. Because it’s a string array, Okta’s EL is written as ‘Arrays.contains(user._, _)’. This group rule automatically adds users with both certs to the ‘IAM Engineering’ group.

<br />

<img src="https://i.imgur.com/IMAGE13.png" alt="IAM Engineering Group Rule">

<br /><br />

This is the group rule for ‘IT Help Desk’. It states that users with either ‘Monica’ as their manager or are interns, will be automatically added.

<br />

<img src="https://i.imgur.com/IMAGE14.png" alt="Help Desk Group Rule">

<br /><br />

The results of the Identity Engine evaluating the environment (i.e. group rules).

<br />

<img src="https://i.imgur.com/IMAGE15.png" alt="Group Rule Results">
