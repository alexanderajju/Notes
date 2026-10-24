
```python

from flask import Flask, jsonify, request
import py_eureka_client.eureka_client as eureka_client
from flask_jwt_extended import (
    JWTManager, create_access_token,
    jwt_required, get_jwt_identity
)
import datetime

app = Flask(__name__)

# JWT Secret Key
app.config["JWT_SECRET_KEY"] = "super-secret-key"  # change in production
app.config["JWT_ACCESS_TOKEN_EXPIRES"] = datetime.timedelta(hours=1)
jwt = JWTManager(app)

# Dummy user store (replace with DB in production)
USERS = {
    "aju": "password123",
    "admin": "adminpass"
}

# Eureka settings
EUREKA_SERVER = "http://EurekaSrvr:0scarPWDisTheB3st@10.10.11.66:8761/eureka/"
APP_NAME = "my-flask-service"
INSTANCE_PORT = 9000

# Register with Eureka
eureka_client.init(
    eureka_server=EUREKA_SERVER,
    app_name=APP_NAME,
    instance_port=INSTANCE_PORT,
    instance_ip="10.10.14.14",  # change to host IP in deployment
    instance_host="10.10.14.14",
    health_check_url=f"http://10.10.14.14:{INSTANCE_PORT}/health",
    home_page_url=f"http://10.10.14.14:{INSTANCE_PORT}/",
    status_page_url=f"http://10.10.14.14:{INSTANCE_PORT}/status",
)

@app.route("/")
def home():
    return jsonify({"message": "Hello from Flask service!"})

@app.route("/status")
def status():
    return jsonify({"status": "UP"})

@app.route("/health")
def health():
    return "OK", 200

# ----------------------------
# LOGIN ENDPOINT
# ----------------------------
@app.route("/login", methods=["POST"])
def login():
    data = request.json
    username = data.get("username")
    password = data.get("password")

    # Validate user
    print(">>>>>>>>>>>>data",data)
    return jsonify({"error": "Invalid username or password"}), 401

# Protected logic endpoint
@app.route("/logic", methods=["POST"])
@jwt_required()
def logic():
    current_user = get_jwt_identity()
    data = request.json
    return jsonify({
        "user": current_user,
        "received": data,
        "processed_by": APP_NAME
    })

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=INSTANCE_PORT)


```



```json
{"instance":{"instanceId":"host.docker.internal:webservice:8082","app":"WEBSERVICE","appGroupName":null,"ipAddr":"192.168.2.1","sid":"na","homePageUrl":"http://host.docker.internal:8082/","statusPageUrl":"http://host.docker.internal:8082/actuator/info","healthCheckUrl":"http://host.docker.internal:8082/actuator/health","secureHealthCheckUrl":null,"vipAddress":"webservice","secureVipAddress":"webservice","countryId":1,"dataCenterInfo":{"@class":"com.netflix.appinfo.InstanceInfo$DefaultDataCenterInfo","name":"MyOwn"},"hostName":"host.docker.internal","status":"UP","overriddenStatus":"UNKNOWN","leaseInfo":{"renewalIntervalInSecs":30,"durationInSecs":90,"registrationTimestamp":0,"lastRenewalTimestamp":0,"evictionTimestamp":0,"serviceUpTimestamp":0},"isCoordinatingDiscoveryServer":false,"lastUpdatedTimestamp":1630906180645,"lastDirtyTimestamp":1630906182808,"actionType":null,"asgName":null,"port":{"$":8082,"@enabled":"true"},"securePort":{"$":443,"@enabled":"false"},"metadata":{"management.port":"8082"}}}
```


'{ 
  "instance": {
    "instanceId": "s3c",
    "hostName": "10.10.14.14",
    "app": "USER-MANAGEMENT-SERVICE",
    "ipAddr": "10.10.14.14",
    "vipAddress": "USER-MANAGEMENT-SERVICE",
    "status": "UP",
    "port": {   
      "$": 9000,
      "@enabled": "true"
    },                 
    "dataCenterInfo": {                                                  
      "@class": "com.netflix.appinfo.InstanceInfo$DefaultDataCenterInfo",
      "name": "MyOwn"
    }
  }
}'