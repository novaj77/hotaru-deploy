# hotaru-deploy

hotaruクラスタに入れるもの（アプリとアドオン）をhelmfileでまとめたリポジトリ

## CI/CD

- PRでは、CIで`helmfile template`を実行して、エラーが無いか確かめる
- アプリケーションがマージされたら、ECRにpushされたイメージのtagに書き換えるPRを自動で出す
- そのPRをマージすると、CIがアプリケーションをクラスタにデプロイする

## 使用技術

- Helm・helmfile：下の4つのreleaseを、helmfile.yamlでまとめて入れる
- GitHub Actions・GitHub App：CI/CDと、リポをまたぐPRの作成

### release

- hotaru-api：アプリケーション本体。自作のchart（Deployment・Service・Ingress）
- AWS Load Balancer Controller：IngressからALBを作り、HTTPSで受けてPodに届ける
- external-dns：Ingressのホスト名を、ALBを指すレコードとしてRoute 53に登録する
- cluster-autoscaler：Podが入りきらないときにノードを増やし、空いたら減らす
