# household-core

こちら(http://ec2-18-222-240-220.us-east-2.compute.amazonaws.com:8080/) のサイトからアクセスしていただくと、成果物を確認できるようになっております。デプロイモードで起動するまでには至らなかったため、レスポンスが遅くなっています。何卒ご了承ください。
こちらはログイン機能が付いています。テストユーザーのアカウントへのログインは以下のメールアドレスとパスワードで可能です。

メールアドレス : testuser@example.com
パスワード : testUser_test
sign up から新規アカウントも作成することもできます。その際のメールアドレスは実在しないものでも大丈夫です。

### 実装した機能
実装した機能といたしましては以下の通りです。
- 買ったものと値段の閲覧・入力・更新・削除ができる
- 費目の追加・削除・編集機能
- 月次集計・年次集計
- ユーザー名の編集
- グループ機能

グループ機能に関しては、まだ完璧ではない状態です。グループに所属すると、共有はできるものの、表示されるものは全てグループでの家計簿だけになってしまい、個人だけのものが見れないといった状況です。

### 利用した技術
- Docker , Docker-compose
- Rails (バックエンド)
- Vue.js (フロント)
- MySQL (データベース)
- Auth0 (認証)

### アプリの動作方法
1. githubから、housegold-core,housegold-api,housegold-frontをそれぞれcloneします。
2. cloneしたのち、ディレクトリ構造を以下のようにします。
housegold-core
    |_  api   
    |_  front
    |_  mysql
    |_  sql
    |_  docker-compose.yml    
    |_  README.md
3. household-coreのディレクトリに移動し、次のコマンドを実行する(時間がかかります)。       
   docker-compose build
4. docker-compose.ymlを開き、15行目( command: npm run serve )をコメントアウトします。
5. docker-compose up -d　を実行する
6. docker ps を実行し、IMAGEがhouseholdcore_freee-apiのCONTAINER IDをコピーします。
7. docker exec -it "コンテナのID"  /bin/sh　を実行
8. rake db:migrate:reset　を実行後、exitを実行
9. docker ps を実行し、IMAGEがnode:12.4.0-alpine のCONTAINER IDをコピーします。
10. docker exec -it "コンテナのID"  /bin/sh　を実行
11. npm install　を実行後、exitを実行
12. docker-compose.ymlを開き、15行目( command: npm run serve )のコメントアウトを外します。
13. docker psで表示されたIDをコピーし以下のコマンドを実行
     docker stop 表示されたID1  表示されたID2  表示されたID3
14. docker ps で全てが表示されなくなったことを確認後、docker-compose up -d　を実行
15. ブラウザを開き localhost:8080 にアクセスする。

