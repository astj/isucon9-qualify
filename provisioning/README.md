# isucon9 provisioning

ansible 2.8.3のみで動作確認しています。

# prerequires
See also: http://isucon.net/archives/53805209.html

- 初期データの作成はローカルで行ってください
- 画像データの展開は ansible 先のインスタンスで取得するので明示的な実行は不要です
  - ローカルに必要になった場合はローカルには手で準備してください

# env

AWS EC2 + ubuntu/images/hvm-ssd/ubuntu-bionic-18.04-amd64-server-20200611 (ami-0cfa3caed4b487e77) AMI で構築しています。

# playbooks

- webapp.yml
  - 競技用
- bench.yml
  - ベンチマーカー用
  - 競技者向け開発用の外部サービスもここから提供するように変更しています

## 競技用サーバのセットアップ

inventory/hostsのwebappセクションに対象のホストを追加してansible-playbookコマンドを実行してください。

```
ansible-playbook webapp.yml -i inventory/hosts
```

## ベンチマーカーサーバのセットアップ

inventory/hostsのbenchセクションに対象のホストを追加してansible-playbookコマンドを実行してください。

```
ansible-playbook bench.yml -i inventory/hosts
```
