# mlflow with Basic Nginx Auth

---

1. Mlflow webserver.
2. Mlflow metastore on postgresql.
3. Mlflow artifacts on a s3 or minio bucket.

More references on this repo: https://github.com/sachua/mlflow-docker-compose

In this repo, is just "attach" mlflow with nginx without other components, feel free to change minio to s3 bucket or other database.

**Config:**

Just change the `.env` file values with respective credentials and `/nginx/.htpasswd`.

Nginx passwd file, you can generate new one in this site: https://www.web2generators.com/apache-tools/htpasswd-generator, and replace current value on the file for a simple http basic auth.

Current have user with 123 password in the file.

After changes, just run `docker compose build && docker compose up`, and go to http://localhost:5000 (you can change this btw).

After docker running, you can tracking with this sample code:

```py
import mlflow

# NGINX Password Auth for MLFLOW in Env variable
# Details at: https://mlflow.org/docs/latest/auth/index.html
os.environ["MLFLOW_TRACKING_USERNAME"] = "user"
os.environ["MLFLOW_TRACKING_PASSWORD"] = "123"

# Tracking Uri
mlflow.set_tracking_uri(f"http://localhost:5000/")
print(f"Tracking Server URI: '{mlflow.get_tracking_uri()}'")

```