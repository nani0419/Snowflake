# Roles
    - AccountAdmin
    - SysAdmin
    - SecurityAdmin
    - UserAdmin

## Discretionary Access Control (DAC)
    - You create it, You own it.
    - Because of the combination of RBAC* and DAC in Snowflake, when we create something, the ROLE we were using at the time we created it, is the role that OWNS it
*RBAC - Role Based Access Control

## Higher Roles Have Custodial Oversight
Think of ACCOUNTADMIN as a sort of "parent" of SYSADMIN, with "custodial rights." SYSADMIN can create a database and by creating it, they are the OWNER of that database. But because SYSADMIN is a "child" of ACCOUNTADMIN, ACCOUNTADMIN can take the database away from SYSADMIN and give it to a SECURITYADMIN if they want to.

ACCOUNTADMIN can also delete something owned by SYSADMIN, rename it, or carry out any other task on anything created or owned by SYSADMIN. SYSADMIN cannot do the same things to items owned by ACCOUNTADMIN. 

## Default Role Assignment
Totally unrelated to any other rules of ROLE design, hierarchy, inheritance, BOGO, or custodial oversight, there is the concept of a DEFAULT ROLE. This is a USER setting that is designed for convenience. Each USER has a role assigned as their default. The default role that has been assigned to you as a Trial Account User is the ACCOUNTADMIN role. This just means that each time you log in to Snowflake, your role will be set to ACCOUNTADMIN. You can change your default role to something different but we don't recommend you do that for your trial account because we have written the workshop labs with the presumption that you will use ACCOUNTADMIN for most tasks. 

## Role Hierarchy Rules Review
If two ROLES are linked by a blue line: 

- The higher role can be DIRECTLY given to a USER and the USER will automatically (BOGO!) be awarded all the lower roles in the same org chart or family tree.
- If a USER has a higher role, they will be able to impersonate all lower ROLES in the same linked tree, without being explicitly given those ROLES.  
- The higher role has custodial oversight of all objects OWNED by a linked, lower role.
- Each USER has a default role they are assigned. This is the ROLE they are set to each time they log in. It doesn't do much more than that, so it is convenience, only and does not affect the current role a user is using. 