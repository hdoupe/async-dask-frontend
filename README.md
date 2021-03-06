Env setup
```
conda create -y -n tc-dask-demo python=3.6 taxcalc dask tornado -c ospc
source activate tc-dask-demo
pip install gunicorn falcon requests httpie
```

In window 1, run
`source activate tc-dask-demo && python dask_rest_api.py`

In window 2, run
`source activate tc-dask-demo && gunicorn mock_pb:api`

In window3, test with:
`source activate tc-dask-demo && http -f POST http://localhost:8888/taxcalc policy='{"2018": {"_II_em": [8000]}}'`


OR run with docker:


```
docker-compose up
```


OR run with kubernetes:

1. Follow [Dask's Kubernetes and Helm guide](http://dask.pydata.org/en/latest/setup/kubernetes-helm.html) to get
kubernetes running on a cloud provider of your choice. This project is developed
with Google cloud in mind.
2. Set up a google cloud cluster and run:
```
helm install pbrain-charts/pbrain -f pbrain/values.yaml
```


Testing:

```
docker-compose run tornado py.test -v
```
