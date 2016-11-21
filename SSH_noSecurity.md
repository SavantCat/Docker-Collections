#Ubuntu SSH

---

```bash
#Dockerfile

FROM ubuntu:16.04 #<-好きなバージョン

RUN apt-get update

RUN apt-get install -y openssh-server nano
RUN mkdir /var/run/sshd

RUN echo 'root:root' |chpasswd

RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

EXPOSE 22

CMD    ["/usr/sbin/sshd", "-D"]
```
---

##注意点
* セキュリティ対策はデフォルト設定の為，注意
* [~]->自分で設定したパラメータに置き換える.　　[]はいらない

---

##手順：Docker
1. 上記のコードをDockerfileという名前で保存
2. cd Dockerfileがある場所へ
3. docker build -t 自分の名前/Liunxの名前:バージョン番号 ./
  * イメージを作成
4. docker run -d -P --name test_sshd [コンテナIDor名前]
  * コンテナ作成
5. docker ps
  * 22ポートへ変換するLocalhostのポート番号を確認

---

##手順：SSH
1. ssh接続開始
2. ssh [ログインID]@localhost -p [確認したポート番号]
  * ログインID：root
  * ログインPW：root

---

参考
* [rastasheep/ubuntu-sshd](https://hub.docker.com/r/rastasheep/ubuntu-sshd/)
* [コマンド集](http://paiza.hatenablog.com/entry/docker_intro)
