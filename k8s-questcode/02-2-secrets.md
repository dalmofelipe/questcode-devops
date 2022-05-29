
# Secrets

Atlas MongoDB
https://www.mongodb.com/atlas/database

API do Github
https://docs.github.com/pt/rest/guides/getting-started-with-the-rest-api


### Atlas MongoDB String Conn

- mongodb+srv://<username>:<password>@<cluster-name>/<dbname>


# Codificando chaves em base64

```bash
echo -n <algum-texto> | base64 -w 0
```


# DEcodificando base64

```bash
echo -n <texto-encodado> | base64 -d
echo -n <texto-encodado> | base64 -d -i
echo -n <texto-encodado> | base64 --decode
```


# k8s Secrets

```yaml

---
apiVersion: v1
kind: Secret
metadata:
  name: questcode
  namespace: staging
type: Opaque
data:
  MONGO_URI: <stringconn-em-base64>
  SECRET_OR_KEY: <secrets-do-app-em-base64>
  GITHUB_CLIENT_SECRET: <github-client-secret-em-base64>
---
apiVersion: v1
kind: Secret
metadata:
  name: questcode
  namespace: prod
type: Opaque
data:
  MONGO_URI: <stringconn-em-base64>
  SECRET_OR_KEY: <secrets-do-app-em-base64>
  GITHUB_CLIENT_SECRET: <github-client-secret-em-base64>
---

```


