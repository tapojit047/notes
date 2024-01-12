# Druid Security
- You can configure authentication and authorization to control access to the Druid APIs.
- Make the configuration changes in the `common.runtime.properties` file on all Druid servers in the cluster.
- Within Druid's operating context, authenticators control the way user identities are verified.
- Authorizers employ user roles to relate authenticated users to the datasources they are permitted to access. You can set the finest-grained permissions on a per-datasource basis.

## Enable an authenticator:
- `druid.extensions.loadList=["druid-basic-security", "druid-histogram", "druid-datasketches", "druid-kafka-indexing-service"]`
```makefile
# Druid basic security
druid.auth.authenticatorChain=["MyBasicMetadataAuthenticator"]
druid.auth.authenticator.MyBasicMetadataAuthenticator.type=basic

# Default password for 'admin' user, should be changed for production.
druid.auth.authenticator.MyBasicMetadataAuthenticator.initialAdminPassword=password1

# Default password for internal 'druid_system' user, should be changed for production.
druid.auth.authenticator.MyBasicMetadataAuthenticator.initialInternalClientPassword=password2

# Uses the metadata store for storing users.
# You can use the authentication API to create new users and grant permissions
druid.auth.authenticator.MyBasicMetadataAuthenticator.credentialsValidator.type=metadata

# If true and if the request credential doesn't exist in this credentials store,
# the request will proceed to next Authenticator in the chain.
druid.auth.authenticator.MyBasicMetadataAuthenticator.skipOnFailure=false

druid.auth.authenticator.MyBasicMetadataAuthenticator.authorizerName=MyBasicMetadataAuthorizer

# Escalator
druid.escalator.type=basic
druid.escalator.internalClientUsername=druid_system
druid.escalator.internalClientPassword=password2
druid.escalator.authorizerName=MyBasicMetadataAuthorizer

druid.auth.authorizers=["MyBasicMetadataAuthorizer"]

druid.auth.authorizer.MyBasicMetadataAuthorizer.type=basic
```

- **authenticatorChain**: An authenticator chain is typically a list of one or more authenticators that are executed sequentially to authenticate clients or users before they are granted access to the system's resources. Each authenticator in the chain has a specific role and may perform different types of authentication. The order in which they are listed in the chain is important because the authentication process stops as soon as one of the authenticators in the chain succeeds.
- **MyBasicMetadataAuthenticator**: A custom or user-defined authenticator for handling authentication and security in a Druid cluster.