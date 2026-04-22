# 📋 DevOps Cheat Sheets

> Referência rápida para os comandos mais usados no dia a dia. Salve e consulte sempre que precisar!

---

## Índice

- [🐳 Docker](#-docker)
- [☸️ kubectl](#️-kubectl)
- [🌿 Git](#-git)
- [🏗️ Terraform](#️-terraform)

---

## 🐳 Docker

### Imagens

| Comando | Descrição |
|---|---|
| `docker pull nginx` | Baixa imagem do Docker Hub |
| `docker images` | Lista imagens locais |
| `docker build -t app:1.0 .` | Build da imagem com tag |
| `docker push user/app:1.0` | Envia imagem para o registry |
| `docker rmi nginx` | Remove imagem local |
| `docker image prune` | Remove imagens sem uso |

### Containers

| Comando | Descrição |
|---|---|
| `docker run -d -p 80:80 nginx` | Roda em background e mapeia porta |
| `docker run -it ubuntu bash` | Modo interativo com terminal |
| `docker ps` | Lista containers em execução |
| `docker ps -a` | Lista todos (incluindo parados) |
| `docker stop [id]` | Para o container |
| `docker rm [id]` | Remove o container |
| `docker restart [id]` | Reinicia o container |

### Logs e Inspeção

| Comando | Descrição |
|---|---|
| `docker logs [id]` | Exibe logs do container |
| `docker logs -f [id]` | Segue logs em tempo real |
| `docker inspect [id]` | Detalhes completos em JSON |
| `docker stats` | Uso de CPU/RAM em tempo real |
| `docker exec -it [id] sh` | Abre shell dentro do container |
| `docker top [id]` | Processos rodando no container |

### Volumes e Redes

| Comando | Descrição |
|---|---|
| `docker volume create vol1` | Cria volume nomeado |
| `docker volume ls` | Lista volumes |
| `docker run -v vol1:/data app` | Monta volume no container |
| `docker network ls` | Lista redes |
| `docker network create mynet` | Cria rede customizada |
| `docker run --network mynet app` | Conecta container à rede |

### Docker Compose

| Comando | Descrição |
|---|---|
| `docker compose up` | Sobe todos os serviços |
| `docker compose up -d` | Em background (detached) |
| `docker compose down` | Para e remove containers |
| `docker compose down -v` | Remove também os volumes |
| `docker compose logs -f` | Segue logs de todos os serviços |
| `docker compose build` | Reconstrói as imagens |
| `docker compose ps` | Status dos serviços |

### Limpeza do Sistema

| Comando | Descrição |
|---|---|
| `docker system prune` | Remove tudo que não está em uso |
| `docker system prune -a` | Inclui imagens não referenciadas |
| `docker system df` | Espaço em disco utilizado |
| `docker container prune` | Remove containers parados |
| `docker volume prune` | Remove volumes não utilizados |

> 💡 **Dica:** Use sempre `--name` para nomear seus containers e `--restart=always` para containers que devem reiniciar automaticamente após reboot do host.

---

## ☸️ kubectl

### Contexto e Cluster

| Comando | Descrição |
|---|---|
| `kubectl config get-contexts` | Lista todos os contextos |
| `kubectl config use-context [ctx]` | Troca de contexto/cluster |
| `kubectl config current-context` | Exibe o contexto atual |
| `kubectl cluster-info` | Informações do cluster |
| `kubectl get nodes` | Lista os nós do cluster |
| `kubectl top nodes` | Uso de recursos dos nós |

### Pods

| Comando | Descrição |
|---|---|
| `kubectl get pods` | Lista pods no namespace padrão |
| `kubectl get pods -A` | Pods em todos os namespaces |
| `kubectl get pods -o wide` | Com IP e nó exibidos |
| `kubectl describe pod [name]` | Detalhes e eventos do pod |
| `kubectl delete pod [name]` | Remove o pod |
| `kubectl exec -it [pod] -- sh` | Shell dentro do pod |
| `kubectl top pods` | Uso de CPU/RAM por pod |

### Deployments

| Comando | Descrição |
|---|---|
| `kubectl get deployments` | Lista deployments |
| `kubectl create deployment app --image=nginx` | Cria deployment |
| `kubectl scale deployment app --replicas=3` | Escala réplicas |
| `kubectl rollout restart deploy/app` | Reinicia pods do deployment |
| `kubectl rollout status deploy/app` | Status do rollout |
| `kubectl rollout undo deploy/app` | Rollback para versão anterior |
| `kubectl set image deploy/app c=img:2.0` | Atualiza imagem do container |

### Services e Ingress

| Comando | Descrição |
|---|---|
| `kubectl get services` | Lista serviços |
| `kubectl expose deploy/app --port=80` | Cria service para deployment |
| `kubectl port-forward pod/[name] 8080:80` | Porta local → pod |
| `kubectl get ingress` | Lista ingresses |
| `kubectl get endpoints` | IPs dos pods por service |

### Namespaces e Manifiestos

| Comando | Descrição |
|---|---|
| `kubectl get ns` | Lista namespaces |
| `kubectl create ns staging` | Cria namespace |
| `kubectl -n staging get pods` | Pods em namespace específico |
| `kubectl apply -f manifest.yaml` | Aplica manifesto |
| `kubectl delete -f manifest.yaml` | Remove recursos do manifesto |
| `kubectl get configmaps` | Lista ConfigMaps |
| `kubectl get secrets` | Lista Secrets |

### Logs e Debugging

| Comando | Descrição |
|---|---|
| `kubectl logs [pod]` | Logs do pod |
| `kubectl logs -f [pod]` | Segue logs em tempo real |
| `kubectl logs [pod] --previous` | Logs do container anterior |
| `kubectl get events --sort-by=.lastTimestamp` | Eventos ordenados por tempo |
| `kubectl describe node [name]` | Detalhes do nó (CPU, Memória) |
| `kubectl run debug --image=busybox -it` | Pod temporário para debug |

> 💡 **Dica:** Adicione ao seu `~/.bashrc`: `alias k=kubectl` e rode `kubectl completion bash >> ~/.bashrc` para autocompletar. Economiza muito tempo no dia a dia.

---

## 🌿 Git

### Configuração Inicial

| Comando | Descrição |
|---|---|
| `git config --global user.name "Seu Nome"` | Define nome do usuário |
| `git config --global user.email "email@email.com"` | Define email |
| `git config --list` | Exibe configurações atuais |
| `git init` | Inicia repositório local |
| `git clone [url]` | Clona repositório remoto |

### Commits e Stage

| Comando | Descrição |
|---|---|
| `git status` | Estado dos arquivos |
| `git add .` | Adiciona tudo ao stage |
| `git add [arquivo]` | Adiciona arquivo específico |
| `git commit -m "feat: mensagem"` | Commita com mensagem |
| `git commit --amend` | Edita o último commit |
| `git diff` | Mostra mudanças não commitadas |
| `git log --oneline` | Histórico resumido |

### Branches

| Comando | Descrição |
|---|---|
| `git branch` | Lista branches locais |
| `git branch -a` | Lista todas (incluindo remotas) |
| `git checkout -b feature/x` | Cria e muda para nova branch |
| `git switch feature/x` | Muda de branch (forma moderna) |
| `git branch -d feature/x` | Deleta branch local |
| `git push origin --delete feature/x` | Deleta branch remota |
| `git branch -m novo-nome` | Renomeia branch atual |

### Merge e Rebase

| Comando | Descrição |
|---|---|
| `git merge feature/x` | Merge da branch no branch atual |
| `git merge --no-ff feature/x` | Merge sempre com commit de merge |
| `git rebase main` | Reaplica commits sobre a main |
| `git rebase -i HEAD~3` | Rebase interativo (squash, etc.) |
| `git cherry-pick [hash]` | Aplica commit específico |
| `git rebase --abort` | Cancela rebase em curso |

### Remote e Sincronização

| Comando | Descrição |
|---|---|
| `git remote -v` | Lista remotes configurados |
| `git remote add origin [url]` | Adiciona remote |
| `git fetch origin` | Baixa mudanças sem aplicar |
| `git pull origin main` | Fetch + merge |
| `git push origin main` | Envia commits para o remote |
| `git push -u origin feature/x` | Push e define upstream |
| `git push --force-with-lease` | Force push seguro |

### Stash e Reset

| Comando | Descrição |
|---|---|
| `git stash` | Salva mudanças temporariamente |
| `git stash pop` | Recupera último stash |
| `git stash list` | Lista stashes salvos |
| `git reset HEAD~1` | Desfaz último commit (mantém arquivos) |
| `git reset --hard HEAD~1` | Desfaz commit e todas as mudanças |
| `git revert [hash]` | Cria commit que desfaz outro |
| `git restore [arquivo]` | Descarta mudanças no arquivo |

> 💡 **Conventional Commits:** Use prefixos padronizados — `feat:` nova funcionalidade, `fix:` correção, `chore:` manutenção, `docs:` documentação, `ci:` pipeline. Facilita a geração de changelog automático.

---

## 🏗️ Terraform

### Comandos Principais

| Comando | Descrição |
|---|---|
| `terraform init` | Inicializa providers e backend |
| `terraform plan` | Visualiza mudanças sem aplicar |
| `terraform apply` | Aplica a infraestrutura |
| `terraform apply -auto-approve` | Aplica sem confirmação manual |
| `terraform destroy` | Destrói toda a infraestrutura |
| `terraform validate` | Valida a sintaxe dos arquivos |
| `terraform fmt` | Formata os arquivos `.tf` |

### State Management

| Comando | Descrição |
|---|---|
| `terraform state list` | Lista recursos no state |
| `terraform state show [resource]` | Detalhes de um recurso |
| `terraform state mv [src] [dst]` | Move recurso no state |
| `terraform state rm [resource]` | Remove do state sem deletar |
| `terraform state pull` | Baixa state remoto |
| `terraform refresh` | Sincroniza state com a infra real |

### Workspaces

| Comando | Descrição |
|---|---|
| `terraform workspace list` | Lista workspaces |
| `terraform workspace new staging` | Cria workspace staging |
| `terraform workspace select prod` | Muda para workspace prod |
| `terraform workspace show` | Exibe workspace atual |
| `terraform workspace delete staging` | Remove workspace |

### Plan com Opções

| Comando | Descrição |
|---|---|
| `terraform plan -out=plan.tfplan` | Salva plano em arquivo |
| `terraform apply plan.tfplan` | Aplica plano salvo |
| `terraform plan -target=aws_instance.web` | Planeja recurso específico |
| `terraform apply -target=module.vpc` | Aplica módulo específico |
| `terraform plan -var-file=prod.tfvars` | Usa arquivo de variáveis |
| `terraform plan -var="env=prod"` | Passa variável inline |

### Output e Import

| Comando | Descrição |
|---|---|
| `terraform output` | Exibe outputs definidos |
| `terraform output -json` | Outputs em formato JSON |
| `terraform import [resource] [id]` | Importa recurso existente |
| `terraform graph` | Gera grafo de dependências |
| `terraform providers` | Lista providers utilizados |
| `terraform version` | Versão do Terraform instalada |

### Estrutura Recomendada de Módulo

```
meu-modulo/
├── main.tf          # Recursos principais
├── variables.tf     # Declaração de variáveis
├── outputs.tf       # Valores exportados
├── providers.tf     # Configuração de providers
├── versions.tf      # Restrições de versão
├── terraform.tfvars # Valores das variáveis (não commitar!)
└── backend.tf       # Configuração do state remoto
```

> 💡 **Boas práticas:** Nunca commite o `terraform.tfstate`. Use backend remoto (S3 + DynamoDB na AWS) para state locking em equipes. Em pipelines CI/CD, use sempre `-out` no `plan` e aplique o arquivo gerado — isso garante que o `apply` executa exatamente o que foi planejado.

---

<div align="center">

Parte do [🚀 DevOps Roadmap — Do Zero ao Profissional](../README.md)

**Encontrou algo errado ou quer adicionar um comando? [Abra um PR!](../CONTRIBUTING.md)**

</div>
