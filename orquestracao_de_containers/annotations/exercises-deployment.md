kubectl create -f deployment.yaml --save-config
kubectl get all
kubectl rollout status deployment/nginx-dp
kubectl rollout history deployment/nginx-dp
kubectl delete deployment nginx-dp
passando a flag --record, o kubernetes vai salvar a causa da mudança no history do rollout
ex.:
```bash
REVISION  CHANGE-CAUSE
1         kubectl create --filename=deployment.yaml --save-config=true --record=true
```
kubectl create -f deployment.yaml --save-config --record
kubectl rollout history deployment/nginx-dp

também é possível ver o histórico de mudanças com o comando describe, que mostra o histórico de mudanças e a causa da mudança na chave Annotations.
kubectl describe deployment nginx-dp 

apos mudar alguma config no arquivo deployment.yaml:
kubectl apply -f deployment.yaml 

Agora vai aparecer a nova revisão no history e adicionar a revisão 2.
kubectl rollout history deployment/nginx-dp       

Também é possível ver o histórico de eventos, que vai mostrar o que aconteceu com o deployment, por exemplo: Pods que subiram e/ou foram deletados.

Comando get eventos:

```bash
kubectl get events 
```

Ver eventos de um deployment específico:

```bash
kubectl get events --field-selector involvedObject.name=nginx-dp
```

Como setar a imagem de um deployment:

```bash
kubectl set image deployment nginx-dp nginx-container=nginx
```

Pode executar com ou sem o --record:
- Com o --record, o kubernetes vai salvar a causa da mudança no history do rollout
- Sem o --record, o kubernetes não vai salvar a causa da mudança no history do rollout

```bash
kubectl set image deployment nginx-dp nginx-container=nginx:1.17.10
kubectl set image deployment nginx-dp nginx-container=nginx:1.17.10 --record
# quando tem o --recored, esse comando é salvo nas anotações no deployment.

# caso uma atualizações tenha sido feita de forma errada ou causado algum problema, é possível voltar para a versão anterior com o comando:

kubectl rollout undo deployment/nginx-dp

# voltar para uma versão específica

kubectl rollout undo deployment/nginx-dp --to-revision=1

```


### Exercício - Atualizando e Revertendo Deployments

error de ImagePullBackOff: Quando a imagem não é encontrada no repositório, o kubernetes tenta baixar a imagem e não consegue, então o pod fica em estado de erro.

Nesse caso, podemos executar um rollback para a versão anterior, ou corrigir a imagem no arquivo deployment.yaml e aplicar novamente.

```bash
kubectl rollout status deployment/nginx-dp
kubectl rollout history deployment/nginx-dp
kubectl rollout undo deployment/nginx-dp
kubectl rollout undo deployment/nginx-dp --to-revision=X
```

Aumentar escalabilidade do deployment:

```bash
kubectl scale deployment nginx-dp --replicas=10
```