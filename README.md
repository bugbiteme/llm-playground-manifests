# llm-playground-manifests
k8s manifests for the LLM playground for RHCL demo

oc apply -f gitops  

oc wait application/llm-playground -n openshift-gitops --for=jsonpath='{.status.sync.status}'=Synced --timeout=300s

oc create -f k8s/pipelinerun-llm-playground.yaml -n llm-playground
oc create -f k8s/pipelinerun-llm-pol-mon.yaml -n llm-playground

oc wait application/llm-playground -n openshift-gitops --for=jsonpath='{.status.health.status}'=Healthy --timeout=600s
