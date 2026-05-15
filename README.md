# Flask Jenkins Demo

这是一个用于练习 Jenkins + GitHub CI/CD 的最小示例项目。

## 项目说明
- 使用 Python Flask 提供一个 Hello World Web 服务
- 使用 Docker 进行容器化构建
- 使用 Jenkins Pipeline 完成自动拉代码、构建镜像、运行容器
- 使用 GitHub Webhook 在代码推送后自动触发构建

## 运行效果
访问：`http://服务器公网IP:5000/`
返回：`Hello World from Flask + Docker + Jenkins!`

## 本地运行
```bash
pip install -r requirements.txt
python app.py
```

浏览器访问：`http://127.0.0.1:5000/`

## Docker 构建运行
```bash
docker build -t flask-jenkins-demo:latest .
docker run -d --name flask-jenkins-demo-container -p 5000:5000 flask-jenkins-demo:latest
```

浏览器访问：`http://服务器公网IP:5000/`

## Jenkins Pipeline
仓库中已包含 `Jenkinsfile`，Jenkins 可直接读取并执行流水线。

## 注意事项
1. Jenkins 所在机器必须能执行 Docker 命令
2. Jenkins 所在 ECS 的 5000 端口需要放通安全组
3. 如果 5000 端口已被占用，可以把 `Jenkinsfile` 里的 `HOST_PORT` 改成别的端口
# test webhook trigger
# test smee webhook
# test smee webhook123
# test smee webhook456
