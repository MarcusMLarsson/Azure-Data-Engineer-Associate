
<h3> Authentication vs Authorization </h3>
<p> Authentication checks if you are who you are (who are you). Authorization determines what you are allowed to access when we know who you are (what can you do?). </p>

<h3> Logins and Users </h3>
<p> Logins sits at the server, users are defined at the database level. Logins does not really have a function for Azure SQL but do for Azure managed instance. Users can
be linked to a user, Azure Directory or SQL Server Authentication</p>

<h3> Permission </h3>
<p> GRANT/REVOKE/DENY model. I can give someone permission, I can take away permission from someone and I can deny permission to someone. SELECT, INSERT, UPDATE, DELETE
are common expressions. </p>

<pre>
GRANT select on OBJECT::Justice Roaster to diana
GRANT select on SCHEMA::Justice Roaster to diana
GRANT revoke on SCHEMA::Justice Roaster to diana
</pre>
