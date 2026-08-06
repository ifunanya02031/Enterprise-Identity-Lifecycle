# Enterprise Identity Lifecycle

<h2>Lab 1 - Enterprise Identity Environment</h2>

This lab simulates an enterprise identity environment by integrating Active Directory with Okta. The objective is to establish Active Directory as a profile source, configure profile mastering, synchronize identities, and automate group membership using Okta Identity Engine.

<br />

<h2>Environment</h2>

<ul>
  <li>Windows Server 2022</li>
  <li>Active Directory Domain Services</li>
  <li>Okta Workforce Identity Cloud</li>
  <li>Okta AD Agent</li>
</ul>

<br />

<h2>1. Install Active Directory Domain Services</h2>

To simulate an enterprise directory environment, begin by deploying a Windows Server and installing the <b>Active Directory Domain Services (AD DS)</b> role.

<br />

<img src="https://i.imgur.com/IMAGE1.png" width="900"/>

<br /><br />

<h2>2. Promote the Server to a Domain Controller</h2>

After installing AD DS, promote the server to a <b>Domain Controller</b>. This creates the Active Directory forest and allows the server to manage users, groups, and other directory objects.

<br />

<img src="https://i.imgur.com/IMAGE2.png" width="900"/>

<br /><br />

<h2>3. Create Directory Users</h2>

Users are one of many objects stored within Active Directory. In this lab, <b>User2</b> belongs to the <b>dev-ad.com</b> forest.

<br />

<img src="https://i.imgur.com/IMAGE3.png" width="900"/>

<br /><br />

<h2>4. Install the Okta Active Directory Agent</h2>

To synchronize Active Directory with Okta, install the <b>Okta AD Agent</b> on the Domain Controller.

The agent makes outbound connections to Okta and imports directory changes such as users, groups, and profile updates.

<br />

<img src="https://i.imgur.com/IMAGE4.png" width="900"/>

<br /><br />

<h2>5. Configure Active Directory as a Profile Source</h2>

Once the integration is complete, Active Directory becomes an official <b>Profile Source</b>.

Enabling <b>Profile & Lifecycle Sourcing</b> establishes Active Directory as the authoritative owner of imported users.

<br />

<img src="https://i.imgur.com/IMAGE5.png" width="900"/>

<br /><br />

<h2>6. Universal Directory</h2>

Every synchronized directory user becomes an Okta user inside Universal Directory.

Universal Directory centralizes identities from multiple profile sources into a single identity profile.

<br />

<img src="https://i.imgur.com/IMAGE6.png" width="900"/>

<br /><br />

<h2>7. Attribute Mapping</h2>

A user is a collection of attributes.

Attribute Mapping transfers values from one profile source to another. Only synchronize attributes that are required by downstream applications.

<br />

<img src="https://i.imgur.com/IMAGE7.png" width="900"/>

<br /><br />

<h2>8. Attribute-Level Mastering</h2>

Because this user originated from Active Directory, imported attributes are read-only inside Okta.

Attribute-Level Mastering (ALM) allows ownership of individual attributes to move from one profile source to another.

Once ownership changes to Okta, the attribute becomes editable within Okta while Active Directory no longer controls that value.

<br />

<img src="https://i.imgur.com/IMAGE8.png" width="900"/>

<br /><br />

<h2>9. Enterprise Groups</h2>

Create enterprise groups representing organizational roles.

Examples:

<ul>
<li>IAM Engineering</li>
<li>IT Help Desk</li>
<li>Human Resources</li>
</ul>

<br />

<img src="https://i.imgur.com/IMAGE9.png" width="900"/>

<br /><br />

<h2>10. Custom Attributes</h2>

Create a custom attribute named <b>Certs</b> using a <b>String Array</b> with enumerated values.

Using an array allows Identity Engine expressions to evaluate multiple certifications efficiently.

<br />

<img src="https://i.imgur.com/IMAGE10.png" width="900"/>

<br /><br />

<h2>11. Automated Group Rules</h2>

Okta Identity Engine evaluates user attributes continuously.

This rule automatically assigns users possessing both:

<ul>
<li>Okta Certified Professional</li>
<li>Okta Certified Administrator</li>
</ul>

to the <b>IAM Engineering</b> group.

<br />

<img src="https://i.imgur.com/IMAGE11.png" width="900"/>

<br /><br />

Another rule automatically assigns interns or users reporting to <b>Monica</b> to the <b>IT Help Desk</b> group.

<br />

<img src="https://i.imgur.com/IMAGE12.png" width="900"/>

<br /><br />

<h2>12. Validation</h2>

After Identity Engine evaluates each rule, users are automatically placed into the appropriate enterprise groups.

<br />

<img src="https://i.imgur.com/IMAGE13.png" width="900"/>

<br /><br />

<h2>Key Takeaways</h2>

<ul>
<li>Identity begins with authoritative profile sources.</li>
<li>Universal Directory centralizes enterprise identities.</li>
<li>Profile Mastering determines attribute ownership.</li>
<li>Attribute Mapping synchronizes identity data between systems.</li>
<li>Identity Engine evaluates users continuously.</li>
<li>Group Rules automate Role-Based Access Control (RBAC).</li>
</ul>
