---
title:  "kubernetes 환경에서의 배치작업 "
search: false
categories: 
  - kubenetes
  - cronjob
  - schedule
last_modified_at: 2018-08-07T14:00:00+09:00
---

# Kubernetes 배치작업 배포
kubernetes에서는 docker image의 배치작업을 진행 할 수 있다. 


##### cronjob template 예시
``` ruby
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: < job 이름 >
spec:
  schedule: < cron spec>
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - args:
            - < arg1 >
            - < arg2 >
            - < arg3 >
            - ...
            envFrom:
            - secretRef:
                name: < secret 파일명 >
            image: < image이름 >
          restartPolicy: Never
```
