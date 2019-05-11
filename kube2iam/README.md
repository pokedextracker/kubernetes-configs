# Kube2IAM

[kube2iam](https://github.com/jtblin/kube2iam) allows setting IAM permissions
on a pod-level instead of at a node-level.

## Install

Note: replace `<account_id>` with the AWS account ID.

```sh
$ helm upgrade \
  --install \
  --wait \
  --namespace kube-system \
  --set image.tag=0.10.6 \
  --set rbac.create=true \
  --set host.iptables=true \
  --set host.interface=cni+ \
  --set extraArgs.base-role-arn=arn:aws:iam::<account_id>:role/kubernetes/pokedextracker/ \
  --set extraArgs.use-regional-sts-endpoint=true \
  --set extraArgs.verbose=true \
  --set updateStrategy=RollingUpdate \
  kube2iam \
  stable/kube2iam
```

## Testing

```sh
$ cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Pod
metadata:
  name: aws-cli
  labels:
    name: aws-cli
  annotations:
    iam.amazonaws.com/role: kubernetes-pokedextracker-cert-manager
spec:
  restartPolicy: Never
  containers:
  - image: fstab/aws-cli
    command:
      - "sleep"
      - "3600"
    name: aws-cli
EOF
$ kubectl exec aws-cli -- /home/aws/aws/env/bin/aws sts get-caller-identity
```
