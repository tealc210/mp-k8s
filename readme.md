## prerequisites:

- Running kubernetes cluster
- kubectl binary

#### Deploy PayMyBuddy on your node(s) :

For attributes db-user, db-pass and db-root-pass in the file 02_db-secrets.yml, replace the pattern **"<BASE64_ENCRYPTED_VALUE>"**, with the value of the following command :

```
> echo -n '<desired_value_of_each_attribute>' | base64
```

![](images/20250206_223426_base64.png)

Then launch the deployment :

```
> kubectl apply -f 01_pmb-namespace.yml && sleep 2 && for resource in `ls -1 *x*.yml | sort`; do kubectl -n paymybuddy apply -f $resource && sleep 2; done
```

![](images/20250206_225847_deploy.png)

Finally, in order to access your newly deployed PayMyBuddy app, you'll need to get the service port :

`> kubectl get services pmb-app -n paymybuddy -o yaml | grep nodePort | awk '{print $3}'`

![](images/20250210_213408_nodeport.png)

And send a request to your kubernetes node, using this port :


![](images/20250210_224739_k8s_pmb.png)
