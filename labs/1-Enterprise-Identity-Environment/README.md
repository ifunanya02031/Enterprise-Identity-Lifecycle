# Enterprise Identity Lifecycle

This implementation establishes the foundation of an enterprise identity environment. Beginning with Active Directory, we'll establish a directory integration with Okta, configure identity sourcing, synchronize user attributes, and automate access through group-based assignments before moving into authentication, federation, and lifecycle management.

---

In order for users within a directory to synchronize to Okta (i.e. IAM Platform) there must be a connector. The connector is then installed on the Windows Server, with Active Directory. The ‘Okta AD Agent’ makes outbound calls to the internet (i.e. Okta) and pushes/imports directory changes (i.e. new users, groups, etc.).

After successful integration, Active Directory now becomes an official profile source.

One of the configurations to note is ‘Profile & Lifecycle Sourcing’, if checked, AD owns the user. A user is a collection of attributes. Meaning, those attributes (for AD originated users) can not be edited within Okta.

The Universal Directory is a collection of users. Every integrated user becomes an Okta user.

Again, a user is a collection of attributes. Certain attributes already exist within a directory, for example, ‘badPwdCount’. To pull data from a source attribute (i.e. originated attribute) to a destination attribute (i.e. another profile source like Okta) is called Attribute Mapping. Only ‘map’ relevant data/attributes (that’ll contribute to downstream applications).

Because AD owns this user (i.e. an AD user), inheriting its value from AD, the attribute cannot be edited from Okta.

Attribute level mastering (ALM) is the act of specifying the profile source that owns the singular attribute. Here, the source priority becomes Okta.

Since the source priority changed, its now editable from Okta. However, on AD its still ‘editable’ but because Okta is now the owner of this attribute, it’ll ignore whatever the value is on AD, and only respects the value from Okta.

Now, there are 5 groups within this enterprise. The custom groups are: IAM Engineering, IT Help Desk and HR.

‘Certs’ is a custom attribute, created in Profile Editor. This attribute is a string array with enumerated values (which is preferred since it evaluates nicer than a regular string).

User 5 has both Okta Certified Professional and Okta Certified Admin cert.

Now, a group rule is an automated means for group membership. Okta’s Identity Engine is responsible for evaluating the environment surrounding its users. Because it’s a string array, Okta’s EL is written as ‘Arrays.contains(user._, _)’. This group rule automatically adds users with both certs to the ‘IAM Engineering’ group.

This is the group rule for ‘IT Help Desk’. It states that users with either ‘Monica’ as their manager or are interns, will be automatically added.

The results of the Identity Engine evaluating the environment (i.e. group rules).
