São conjuntos de configurações baseados em uma **Base**, onde estão presentes manifestos genéricos e que nas configurações específicos **Dev** ou **Production** por exemplo é possível fazer alterações nessa configuração padrão e usar para consume próprio. 

```ruby
├── base
│   ├── deployment.yaml
│   ├── service.yaml
│   └── kustomization.yaml
└── overlays
    ├── dev
    │   ├── kustomization.yaml
    │   └── patch.yaml
    ├── staging
    │   ├── kustomization.yaml
    │   └── patch.yaml
    └── prod
        ├── kustomization.yaml
        └── patch.yaml
```
