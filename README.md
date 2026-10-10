# hotaru-deploy

hotaruクラスタに入れるもの（アプリとアドオン）をhelmfileでまとめたリポジトリ

- PRでは、CIで`helmfile template`を実行して、エラーが無いか確かめる
- アプリケーションがマージされたら、ECRにpushされたイメージのtagに書き換えるPRを自動で出す
- そのPRをマージすると、CIがアプリケーションをクラスタにデプロイする
