# kubens and kubectx aliases

To switch to the previously used context or namespace:

`k-='kubectx -'`
`k--='kubens -'`

# kubectl-aliases

This repository contains [a script](generate_aliases.py) to generate hundreds of
convenient shell aliases for kubectl, so you no longer need to spell out every single
command and --flag over and over again.

An example shell alias created from command/flags permutation looks like:

    alias ksysgdepwslowidel='kubectl --namespace=kube-system get deployment --watch --show-labels -o=wide -l'

Confused? Read on.

### Examples

Some of the 800 generated aliases are:

```sh
alias k='kubectl'
alias kg='kubectl get'
alias kgpo='kubectl get pod'

alias ksysgpo='kubectl --namespace=kube-system get pod'

alias krm='kubectl delete'
alias krmf='kubectl delete -f'
alias krming='kubectl delete ingress'
alias krmingl='kubectl delete ingress -l'
alias krmingall='kubectl delete ingress --all-namespaces'

alias kgsvcoyaml='kubectl get service -o=yaml'
alias kgsvcwn='watch kubectl get service --namespace'
alias kgsvcslwn='watch kubectl get service --show-labels --namespace'

alias kgwf='watch kubectl get -f'
...
```

See [the full list](.kubectl_aliases).

### Installation

You can directly download the [`.kubectl_aliases` file](https://rawgit.com/ahmetb/kubectl-alias/master/.kubectl_aliases)
and save it in your $HOME directory, then edit your .bashrc/.zshrc file with:

```sh
[ -f ~/.kubectl_aliases ] && source ~/.kubectl_aliases
```

**Print the full command before running it:** Add this to your `.bashrc` or
`.zshrc` file:

```sh
function kubectl() { echo "+ kubectl $@">&2; command kubectl $@; }
```

### Syntax explanation

* **`k`**=`kubectl`
  * **`sys`**=`--namespace kube-system`
* commands:
  * **`g`**=`get`
  * **`d`**=`describe`
  * **`rm`**=`delete`
  * **`a`**:`apply -f`
  * **`ex`**: `exec -i -t`
  * **`lo`**: `logs -f`
* resources:
        ('po', 'pods', ['g', 'd', 'rm'], None),
        ('dep', 'deployment', ['g', 'd', 'rm'], None),
        ('svc', 'service', ['g', 'd', 'rm'], None),
        ('ing', 'ingress', ['g', 'd', 'rm'], None),
        ('cm', 'configmap', ['g', 'd', 'rm'], None),
        ('sec', 'secret', ['g', 'd', 'rm'], None),
        ('no', 'nodes', ['g', 'd'], ['sys']),
        ('ns', 'namespaces', ['g', 'd', 'rm'], ['sys']),
        ('ss', 'statefulset', ['g', 'd', 'rm'], ['sys']),
        ('cbc', 'couchbasecluster', ['g', 'd', 'rm'], ['sys']),
        ('pv', 'persistentvolumes', ['g', 'd', 'rm'], ['sys']),
        ('pvc', 'persistentvolumeclaims', ['g', 'd', 'rm'], ['sys']),
        ('cr', 'clusterroles', ['g', 'd', 'rm'], ['sys']),
        ('crb', 'clusterrolebindings', ['g', 'd', 'rm'], ['sys']),
        ('r', 'roles', ['g', 'd', 'rm'], ['sys']),
        ('rb', 'rolebindings', ['g', 'd', 'rm'], ['sys']),
        ('sc', 'storageclass', ['g', 'd', 'rm'], ['sys']),

  * **`po`**=pod, **`dep`**=`deployment`, **`ing`**=`ingress`,
    **`svc`**=`service`, **`cm`**=`configmap`, **`sec`=`secret`**,
    **`ns`**=`namespace`, **`no`**=`node`, **`ss`**=`statefulset`**,
    **`cbc`**=`couchbasecluster`, **`pv`**=`persistentvolumes`, **`pvc`**=`persistentvolumeclaims`**,
    **`cr`**=`clusterroles`, **`crb`**=`clusterrolebindings`,
    **`r`**=`roles`**, **`rb`**=`rolebindings`**,
    **`sc`**=`storageclass`**
* flags:
  * output format: **`oyaml`**, **`ojson`**, **`owide`**
  * **`all`**: `--all` or `--all-namespaces` depending on the command
  * **`sl`**: `--show-labels`
  * **`w`**=`-w/--watch`
* value flags (should be at the end):
  * **`n`**=`-n/--namespace`
  * **`f`**=`-f/--filename`
  * **`l`**=`-l/--selector`
  
### FAQ

- **Doesn't this slow down my shell start up?** Sourcing the file that contains
~500 aliases takes about 30-45 milliseconds in my shell (zsh). I don't think
it's a big deal for me. Measure it with `echo $(($(date +%s%N)/1000000))`
command yourself in your .bashrc/.zshrc.

- **Can I add more Kubernetes resource types to this?** Please consider forking
  this repo and adding the resource types you want. Not all resource types are
  used by everyone, and adding more resource types slows down shell initialization
  see above).

- **Where can I find PowerShell aliases for kubectl?** There’s a fork of this
  [here](https://github.com/shanoor/kubectl-aliases-powershell).

### Authors

- [@ahmetb](https://twitter.com/ahmetb)

-----

This is not an official Google project.
