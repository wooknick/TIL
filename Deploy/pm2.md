# pm2를 활용한 원격 배포 방법 정리

github에서 바로 배포

1. Local / Remote 모두 pm2 설치
   > npm i -g pm2
2. SSH Key 등록

- local에서 실행. remote에 패스워드 없이 접속하기 위함.

  > \$> ssh-copy-id id@**_._**.**_._**

- remote에서 실행. git에 패스워드 없이 접속해서 소스를 받아오기 위함. 생성된 키를 [Github SSH Keys](https://github.com/settings/keys)에 등록.

> \$> ssh-keygen

> \$> cat ~/.ssh/id_rsa.pub

> \$> ssh -T git@github.com

3. ecosystem.config.js

```javascript
module.exports = {
  apps: [
    {
      name: "appName",
      script: "start.js",
      instances: 0,
      exec_mode: "cluster",
      env: {
        COMMON_VARIABLE: true,
      },
      env_production: {
        NODE_ENV: "production",
      },
    },
  ],

  deploy: {
    production: {
      user: "user",
      host: "host",
      ref: "origin/master",
      repo: "git@github.com:id/repo.git",
      ssh_options: "StrictHostKeyChecking=no",
      path: "/var/www/production",
      "post-deploy":
        "npm install && npm run build && pm2 startOrRestart ecosystem.config.js --env production",
    },
  },
};
```

4. deploy

- 최초 한 번 실행
  > \$> pm2 deploy production setup

> \$> pm2 deploy ecosystem.config.js production

- 지속적 배포
  > \$> pm2 deploy production update
