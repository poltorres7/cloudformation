Commands
==========

#### Instrucciones

##### Lab 1

Crea una VPC en la nube de AWS.
En el template `aws-vpc.yml` se encuentra el IaC para crear una VPC.
A continuación el comando necesario para crearla en tu cuenta.
> Recuerda que antes de ejecutar el comando ya debes haber configurado tu **aws cli** con tu SecretKey y AccessKey de AWS.


```bash
aws cloudformation deploy --template-file aws-vpc.yml \
    --stack-name dev-vpc \
    --parameter-overrides \
    Env=dev VPCName=core CidrBlock=10.0.0.0/16 \
    --tags Env=Dev Course=DevOps
```

![AWS VPC dasboard](https://i.imgur.com/Ldsv261.png)

> [!CUIDADO]
> Recuerda eliminar los recursos creados. Esto se puede hacer
> Eliminando el stack desde la consola de AWS en la sección de cloudformation
