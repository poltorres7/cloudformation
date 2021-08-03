Commands
==========

#### Instrucciones

### Lab 1

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



### Lab 2

- Crea 3 subnets: `publica`, `privada` y de `datos` que viva dentro de la VPC creada en el lab1.
- Crea un internet gateway para habilitar salida a internet.
- Crea una Tabla de ruteo, asocia la tabla a la subnet publica y agrega una regla de salida

Con el siguiente comando y el deploy del template `aws-subnets.yml` podrás crear estos recursos.

```bash
aws cloudformation deploy --template-file aws-subnets.yml \
    --stack-name dev-public-subnet \
    --parameter-overrides \
    Env=dev VPCName=core PublicSubnetCidrBlock=10.0.16.0/22 \
    PrivateSubnetCidrBlock=10.0.0.0/21 \
    DataSubnetCidrBlock=10.0.8.0/21 \
    --tags Env=Dev Course=DevOps
```

> [!TIP]
> Trata de crear una instancia en la subnet publica y conectarte por SSH. Toma un screenshot y subela en el hilo de slack de este laboratorio

> [!NOTE]
> Se realizaron cambios en el template `aws-vpc.yml` necesarios para poder desplegar el template `aws-subnets.yml`

**Subnets**
![Subnets creadas](https://i.imgur.com/yYgsNf4.png)

**Route Tables**
![Tabla de ruteo](https://i.imgur.com/D77oK3E.png)

**Internet Gateway**
![Internet Gateway](https://i.imgur.com/edlQUJP.png)

**Instancia EC2**
![Instancia EC2](https://i.imgur.com/JHVq8Uk.png)

**Conexión a la instancia**
![Conexión a la instancia](https://i.imgur.com/yUwreOX.png)