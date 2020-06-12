
load('ext://namespace', 'namespace_create', 'namespace_inject')
namespace_create('robot-shop')

docker_build('robotshop/rs-cart','./cart')
docker_build('robotshop/rs-catalogue','./catalogue')
docker_build('robotshop/rs-dispatch','./dispatch')
#docker_build('robotshop/rs-load','./load-gen')
docker_build('robotshop/rs-mongodb','./mongo')
docker_build('robotshop/rs-mysql-db','./mysql')
docker_build('robotshop/rs-payment','./payment')
docker_build('robotshop/rs-ratings','./ratings')
docker_build('robotshop/rs-shipping','./shipping')
docker_build('robotshop/rs-user','./user')
docker_build('robotshop/rs-web','./web', live_update=[
  sync('./web/static', '/usr/share/nginx/html')
])

yaml = helm(
  './K8s/helm',
  # The release name, equivalent to helm --name
  name='robot-shop',
  # The namespace to install in, equivalent to helm --namespace
  namespace='robot-shop',
  # The values file to substitute into the chart.
  values=['./K8s/helm/values.yaml'],
  # Values to set from the command-line
  #set=['service.port=1234', 'ingress.enabled=true']
  )
k8s_yaml(yaml)

# Need to access the frontend
k8s_resource('web', port_forwards=8080)