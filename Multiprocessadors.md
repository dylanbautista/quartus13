# Instruccions per installar Quartus i Modelsim

## Dependències
Instal·lar docker. Instruccions aqui:
```
https://docs.docker.com/engine/install/
```

## Setup

Clonar el següent repository:
```bash
git clone https://github.com/aarmejach/quartus13.git
cd quartus13
export QUARTUS_PATH=$PWD
```

Descarregar Quartus II 13.0sp1 Web Edition
```
https://www.intel.com/content/www/us/en/software-kit/711790/intel-quartus-ii-web-edition-design-software-version-13-0sp1-for-linux.html
```

Descomprimir el tar i moure els seguents fitxers a `QUARTUS_PATH`:
```
arria_web-13.0.1.232.qdz
cyclonev-13.0.1.232.qdz
cyclone_web-13.0.1.232.qdz
max_web-13.0.1.232.qdz
ModelSimSetup-13.0.1.232.run
QuartusHelpSetup-13.0.1.232.run
QuartusSetupWeb-13.0.1.232.run
```

Genera la imatge base incloent ModelSim:
```bash
docker build -t quartus_base:13.0.1.2 -f Dockerfile_with_modelsim .
```

Genera la imatge final amb tag `quartus:13.0.1.2` usant com a base la imatge anterior:
```
docker build -t quartus:13.0.1.2 -f Dockerfile_devices --build-arg QUARTUS_BASE=quartus_base:13.0.1.2 .
```

Despres de generar la imatge final es pot borrar la cache:
```
docker builder prune
```

Executar Quartus:
```bash
$QUARTUS_PATH/shell/quartus
```