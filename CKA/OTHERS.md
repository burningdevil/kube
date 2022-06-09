# OTHERS

## kubectl replace vs kubectl apply

kubectl apply .. will use various heuristics to selectively update the values specified within the resource.

kubectl replace ... will replace / overwrite the entire object with the values specified. This should be preferred as you're avoiding the complexity of the selective heuristic update. However some resources like ingresses/load balancers can't really be replaced as they're immutable.

## Management techniques

### Imperative commands

When using imperative commands, a user operates directly on live objects in a cluster. The user provides operations to the kubectl command as arguments or flags.

This is the recommended way to get started or to run a one-off task in a cluster. Because this technique operates directly on live objects, it provides no history of previous configurations.

Examples
Run an instance of the nginx container by creating a Deployment object:

`
kubectl create deployment nginx --image nginx
`

### Impreative object configuration

In imperative object configuration, the kubectl command specifies the operation (create, replace, etc.), optional flags and at least one file name. The file specified must contain a full definition of the object in YAML or JSON format.

See the API reference for more details on object definitions.

**Warning: The imperative replace command replaces the existing spec with the newly provided one, dropping all changes to the object missing from the configuration file. This approach should not be used with resource types whose specs are updated independently of the configuration file. Services of type LoadBalancer, for example, have their externalIPs field updated independently from the configuration by the cluster.**

Examples

```bash
# Create the objects defined in a configuration file:
kubectl create -f nginx.yaml

# Delete the objects defined in two configuration files:
kubectl delete -f nginx.yaml -f redis.yaml

# Update the objects defined in a configuration file by overwriting the live configuration:
kubectl replace -f nginx.yaml
```

### Declarative object configuration

When using declarative object configuration, a user operates on object configuration files stored locally, however the user does not define the operations to be taken on the files. Create, update, and delete operations are automatically detected per-object by kubectl. This enables working on directories, where different operations might be needed for different objects.

Examples

```bash
# Process all object configuration files in the configs directory, and create or patch the live objects. You can first diff to see what changes are going to be made, and then apply:
kubectl diff -f configs/
kubectl apply -f configs/

# Recursively process directories:
kubectl diff -R -f configs/
kubectl apply -R -f configs/
```
