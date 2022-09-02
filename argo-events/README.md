Argo Events:
--------------

Create Workflow Sensor:
------------------------

kubectl apply -n argo-events -f argo-events/sensor-webhook-1.yaml


Use either Curl or Postman to send a post request to the http://localhost:/example:
-------------------------------------------------------------------------------------
curl -d '{"message":"Trigger my workflow"}' -H "Content-Type: application/json" -X POST
 http://localhost:30899/example