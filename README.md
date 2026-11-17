# tiss-day2-gitops

Argo CD 讀的 GitOps repo：叢集「應該長什麼樣子」都寫在這裡。
image 由 [tiss-hello-app](https://github.com/rHuei/tiss-hello-app) 的 GitHub Actions 打包推到 GHCR，
並自動更新 `hello/overlays/lab/kustomization.yaml` 的 `newTag` 與 `VERSION`。

| 目錄 | 內容 |
|---|---|
| hello/base | Deployment、Service、PVC（任何環境都一樣） |
| hello/overlays/lab | namespace、image 版本、ConfigMap、HTTPRoute（apps-gw） |
| platform | NetworkPolicy、RoleBinding |
| apps | hello、platform 兩個 Application（Argo CD Project：fg01） |
| root.yaml | App of Apps 的入口（Project：default，因為 Application 物件放在 argocd namespace） |

本機檢查：`kubectl kustomize hello/overlays/lab`

## Argo CD 需要的設定
- Settings → Repositories：登記本 repo
- Project `fg01`：SOURCE REPOSITORIES 加本 repo；DESTINATIONS 加 `in-cluster` / `fg01`
