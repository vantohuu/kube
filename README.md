# kube

# Các bước triển khai
#### B1: Bật kubenetes trong docker
![image](https://github.com/vantohuu/kube/assets/82772386/36b6313b-ecc0-4bda-9d91-aeb2d72e42eb)

#### B2: Triển khai ingress nginx controller

Thực hiện step 1-3 theo hướng dẫn https://platform9.com/learn/v1.0/tutorials/nginix-controller-via-yaml
Sau khi thực hiện xong 3 bước ta tạo được một namespace ingress-nginx

#### B3: Triển khai các service lên namspace ingress-nginx vừa triển khai xong

clone https://github.com/vantohuu/kube
Vào thư mục kube

- **_Triển khai soa service_**
  - Vao thư mục svc bằng cách: cd svc
  - Triển khai pod
    +  kubectl apply -f 3.pods.yaml --namespace ingress-nginx (nếu muốn xóa cái vừa triển khai thì thay apply thành delete)
  - Triển khai autoscale cho pod
    +  kubectl apply -f 3.pods.soa.hpa.yaml --namespace ingress-nginx (nếu muốn xóa cái vừa triển khai thì thay apply thành delete)
  - Triển khai service 
    +  kubectl apply -f soamain.svc.yaml --namespace ingress-nginx (nếu muốn xóa cái vừa triển khai thì thay apply thành delete)

- **_Triển khai payment service_**
  - Vào thư mục svc bằng cách: cd ../svc-payment
  - Triển khai pod
    +  kubectl apply -f 3.pods.yaml --namespace ingress-nginx (nếu muốn xóa cái vừa triển khai thì thay apply thành delete)
   - Triển khai service 
     +  kubectl apply -f soapayment.svc.yaml --namespace ingress-nginx (nếu muốn xóa cái vừa triển khai thì thay apply thành delete)


- **_Dưa các services lên ingress_**
  - Vao thư mục svc bằng cách: cd ../ingress
    +  kubectl apply -f nginx.ingress.yaml --namespace ingress-nginx (nếu muốn xóa cái vừa triển khai thì thay apply thành delete)

**_Kiểm tra những cái vừa triển khai: kubectl gel all --namespace ingress-nginx_**
![image](https://github.com/vantohuu/kube/assets/82772386/82a6ef55-178a-4967-a04e-c7dc23655ffb)

# Kết quả
Sau khi triển khai ta có được api backend với port:80, host:localhost

